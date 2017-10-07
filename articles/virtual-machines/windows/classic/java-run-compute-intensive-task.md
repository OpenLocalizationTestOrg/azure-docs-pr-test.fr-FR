---
title: application de Java aaaCompute intensif sur une machine virtuelle | Documents Microsoft
description: "Découvrez comment toocreate une machine virtuelle Azure qui exécute une application Java de calcul intensif qui peut être surveillée par une autre application Java."
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: ae6f2737-94c7-4569-9913-d871450c2827
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 02a198802a8d78bd444cd5a9197a78cb94f48e3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-compute-intensive-task-in-java-on-a-virtual-machine"></a>Comment toorun nécessitant une tâche dans Java sur un ordinateur virtuel
> [!IMPORTANT] 
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.

Avec Azure, vous pouvez utiliser une tâche de calcul intensif toohandle machine virtuelle. Par exemple, un ordinateur virtuel peut gérer des tâches et de remettre machines tooclient de résultats ou des applications mobiles. Après avoir lu cet article, vous devez comprendre comment toocreate une machine virtuelle qui exécute une application Java de calcul intensif qui peut être surveillée par une autre application Java.

Ce didacticiel suppose que vous savez comment les applications console toocreate Java, peut importer l’application de bibliothèques tooyour Java et peut générer une archive Java (JAR). Aucune connaissance de Microsoft Azure n'est nécessaire.

Vous apprendrez à effectuer les opérations suivantes :

* Comment toocreate un ordinateur virtuel avec un Kit de développement Java (JDK) déjà installé.
* Comment tooremotely du journal dans la machine virtuelle de tooyour.
* Comment toocreate un service bus espace de noms.
* Comment toocreate une application Java qui effectue une tâche de calcul intensif.
* Comment toocreate une application Java qui surveille hello progression de la tâche de calcul intensif hello.
* Comment toorun hello des applications Java.
* Comment toostop hello des applications Java.

Ce didacticiel utilise hello problème commercial pour la tâche de calcul intensif hello. Hello Voici un exemple de tâche de calcul intensif hello en cours d’exécution hello Java application.

![Résolution du problème du voyageur de commerce][solver_output]

Hello Voici un exemple de tâche de calcul intensif Java application analyse hello de hello.

![Client du problème du voyageur de commerce][client_output]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a>toocreate une machine virtuelle
1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com).
2. Cliquez sur **New**, sur **Compute**, sur **Virtual machine**, puis sur **From Gallery**.
3. Bonjour **sélection d’image de machine virtuelle** boîte de dialogue, sélectionnez **JDK 7 Windows Server 2012**.
   Notez que **JDK 6 Windows Server 2012** au cas où vous avez des applications héritées qui ne sont pas encore prêt toorun JDK 7.
4. Cliquez sur **Suivant**.
5. Bonjour **configuration d’ordinateur virtuel** boîte de dialogue :
   1. Spécifiez un nom pour la machine virtuelle de hello.
   2. Spécifiez toouse de taille hello pour la machine virtuelle de hello.
   3. Entrez un nom pour l’administrateur de hello dans hello **nom d’utilisateur** champ. N’oubliez pas ce nom et hello mot de passe que vous devrez entrer ensuite, vous allez les utiliser lorsque vous vous connectez à distance dans la machine virtuelle de toohello.
   4. Entrez un mot de passe Bonjour **nouveau mot de passe** champ et entrez-la dans hello **confirmer** champ. Il s’agit de mot de passe hello.
   5. Cliquez sur **Suivant**.
6. Bonjour suivant **configuration d’ordinateur virtuel** boîte de dialogue :
   1. Pour **service de cloud computing**, utiliser la valeur par défaut hello **créer un service cloud**.
   2. Hello valeur pour **nom DNS du service Cloud** doit être unique sur cloudapp.net. Si nécessaire, modifiez cette valeur afin qu'Azure indique qu'elle est unique.
   3. Indiquez une région, un groupe d'affinités ou un réseau virtuel. Dans le cadre de ce didacticiel, indiquez une région comme **Bretagne**.
   4. Pour **Storage Account**, sélectionnez **Use an automatically generated storage account**.
   5. Pour **Availability Set**, sélectionnez **(None)**.
   6. Cliquez sur **Suivant**.
7. Bonjour final **configuration d’ordinateur virtuel** boîte de dialogue :
   1. Accepter les entrées de point de terminaison par défaut hello.
   2. Cliquez sur **Terminé**.

## <a name="tooremotely-log-in-tooyour-virtual-machine"></a>journal de tooremotely dans la machine virtuelle de tooyour
1. Ouvrez une session sur toohello [portail Azure classic](https://manage.windowsazure.com).
2. Cliquez sur **Machines virtuelles**.
3. Cliquez sur nom hello hello virtuels que vous souhaitez toolog dans.
4. Cliquez sur **Connecter**.
5. Répondre toohello invites en tant que machine virtuelle de toohello tooconnect nécessaires. À l’invite de mot de passe et le nom de l’administrateur hello, utilisez les valeurs de hello que vous avez fourni lors de la création de la machine virtuelle de hello.

Notez que les fonctionnalités Azure Service Bus hello requiert hello Baltimore CyberTrust Root certificat toobe est installé dans le cadre de votre JRE **cacerts** stocker. Ce certificat est automatiquement inclus dans hello Java Runtime Environment (JRE) utilisé par ce didacticiel. Si vous n’avez pas de ce certificat dans votre JRE **cacerts** stockage, consultez [Ajout d’un toohello certificat magasin de certificats d’autorité de certification Java] [ add_ca_cert] pour plus d’informations sur l’ajout d’il (ainsi que informations sur l’affichage des certificats de hello dans votre magasin cacerts).

## <a name="how-toocreate-a-service-bus-namespace"></a>Comment toocreate un service bus espace de noms
les files d’attente de toobegin à l’aide du Service Bus dans Azure, vous devez d’abord créer un espace de noms de service. Ce dernier fournit un conteneur d’étendue pour l’adressage des ressources Service Bus au sein de votre application.

toocreate un espace de noms de service :

1. Ouvrez une session sur toohello [portail Azure classic](https://manage.windowsazure.com).
2. Dans le volet de navigation inférieure gauche hello Hello portail Azure classic, cliquez sur **Service Bus, contrôle d’accès et la mise en cache**.
3. Dans le volet supérieur gauche de hello Hello portail Azure classic, cliquez sur hello **Service Bus** nœud, puis cliquez sur hello **nouveau** bouton.  
   ![Capture d'écran du nœud Service Bus][svc_bus_node]
4. Bonjour **créer un nouveau Namespace de Service** boîte de dialogue, entrez un **Namespace**, puis toomake assurer qu’il est unique, cliquez sur le **vérifier la disponibilité** bouton.  
   ![Capture d'écran Créer un espace de noms][create_namespace]
5. Après avoir vérifié que le nom d’espace de noms hello est disponible, cliquez sur le pays ou la région dans laquelle votre espace de noms doit être hébergé, puis cliquez sur hello **créer de Namespace** bouton.  
   
   espace de noms de Hello que vous avez créé apparaît dans hello portail Azure classic et prend un tooactivate moment. Attendez que l’état hello est **Active** avant de passer à l’étape suivante de hello.

## <a name="obtain-hello-default-management-credentials-for-hello-namespace"></a>Obtenir hello par défaut gestion des informations d’identification pour l’espace de noms hello
Dans les opérations de gestion de tooperform commande, telles que la création d’une file d’attente, sur hello le nouvel espace de noms, vous avez besoin d’informations d’identification de gestion tooobtain hello pour l’espace de noms.

1. Dans le volet de navigation gauche hello, cliquez sur hello **Service Bus** nœud pour afficher la liste de hello des espaces de noms disponibles.
   ![Capture d'écran Available Namespaces][avail_namespaces]
2. Sélectionnez l’espace de noms hello que vous venez de créer à partir de la liste hello indiqué.
   ![Capture d’écran Liste d’espaces de noms][namespace_list]
3. Hello droite **propriétés** volet répertorie les propriétés hello pour le nouvel espace de noms.
   ![Capture d'écran du volet Propriétés][properties_pane]
4. Hello **clé par défaut** est masqué. Cliquez sur hello **vue** bouton informations d’identification de sécurité toodisplay hello.
   ![Capture d'écran Clé par défaut][default_key]
5. Prenez note de hello **émetteur par défaut** et hello **clé par défaut** car vous utiliserez ces informations ci-dessous tooperform opérations avec l’espace de noms.

## <a name="how-toocreate-a-java-application-that-performs-a-compute-intensive-task"></a>Comment toocreate une application Java qui effectue une tâche de calcul intensif
1. Sur votre ordinateur de développement (qui n’a pas de machine virtuelle de hello toobe que vous avez créés), téléchargement hello [SDK Azure pour Java](https://azure.microsoft.com/develop/java/).
2. Créez une application de console Java à l’aide du code d’exemple hello à fin hello de cette section. Dans ce didacticiel, nous allons utiliser **TSPSolver.java** comme nom de fichier hello Java. Modifier hello **votre\_service\_bus\_espace de noms**, **votre\_service\_bus\_propriétaire**et **votre\_service\_bus\_clé** des espaces réservés toouse service bus **espace de noms**, **émetteur par défaut** et  **Clé par défaut** valeurs, respectivement.
3. Après le codage, exportation hello application tooa exécutable archive Java (JAR) et hello de package requis bibliothèques dans hello généré JAR. Dans ce didacticiel, nous allons utiliser **TSPSolver.jar** comme nom de fichier JAR hello généré.

<p/>

    // TSPSolver.java

    import com.microsoft.windowsazure.services.core.Configuration;
    import com.microsoft.windowsazure.services.core.ServiceException;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import java.io.*;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import java.util.ArrayList;
    import java.util.Date;
    import java.util.List;

    public class TSPSolver {

        //  Value specifying how often tooprovide an update toohello console.
        private static long loopCheck = 100000000;  

        private static long nTimes = 0, nLoops=0;

        private static double[][] distances;
        private static String[] cityNames;
        private static int[] bestOrder;
        private static double minDistance;
        private static ServiceBusContract service;

        private static void buildDistances(String fileLocation, int numCities) throws Exception{
            try{
                BufferedReader file = new BufferedReader(new InputStreamReader(new DataInputStream(new FileInputStream(new File(fileLocation)))));
                double[][] cityLocs = new double[numCities][2];
                for (int i = 0; i<numCities; i++){
                    String[] line = file.readLine().split(", ");
                    cityNames[i] = line[0];
                    cityLocs[i][0] = Double.parseDouble(line[1]);
                    cityLocs[i][1] = Double.parseDouble(line[2]);
                }
                for (int i = 0; i<numCities; i++){
                    for (int j = i; j<numCities; j++){
                        distances[i][j] = Math.hypot(Math.abs(cityLocs[i][0] - cityLocs[j][0]), Math.abs(cityLocs[i][1] - cityLocs[j][1]));
                        distances[j][i] = distances[i][j];
                    }
                }
            } catch (Exception e){
                throw e;
            }
        }

        private static void permutation(List<Integer> startCities, double distSoFar, List<Integer> restCities) throws Exception {

            try
            {
                nTimes++;
                if (nTimes == loopCheck)
                {
                    nLoops++;
                    nTimes = 0;
                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.print("Current time is " + dateFormat.format(date) + ". ");
                    System.out.println(  "Completed " + nLoops + " iterations of size of " + loopCheck + ".");
                }

                if ((restCities.size() == 1) && ((minDistance == -1) || (distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-1)] < minDistance))){
                    startCities.add(restCities.get(0));
                    newBestDistance(startCities, distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-2)]);
                    startCities.remove(startCities.size()-1);
                }
                else{
                    for (int i=0; i<restCities.size(); i++){
                        startCities.add(restCities.get(0));
                        restCities.remove(0);
                        permutation(startCities, distSoFar + distances[startCities.get(startCities.size()-1)][startCities.get(startCities.size()-2)],restCities);
                        restCities.add(startCities.get(startCities.size()-1));
                        startCities.remove(startCities.size()-1);
                    }
                }
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        private static void newBestDistance(List<Integer> cities, double distance) throws ServiceException, Exception {
            try
            {
                minDistance = distance;
                String cityList = "Shortest distance is "+minDistance+", with route: ";
                for (int i = 0; i<bestOrder.length; i++){
                    bestOrder[i] = cities.get(i);
                    cityList += cityNames[bestOrder[i]];
                    if (i != bestOrder.length -1)
                        cityList += ", ";
                }
                System.out.println(cityList);
                service.sendQueueMessage("TSPQueue", new BrokeredMessage(cityList));
            }
            catch (ServiceException se)
            {
                throw se;
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        public static void main(String args[]){

            try {

                Configuration config = ServiceBusConfiguration.configureWithWrapAuthentication(
                        "your_service_bus_namespace", "your_service_bus_owner",
                        "your_service_bus_key",
                        ".servicebus.windows.net",
                        "-sb.accesscontrol.windows.net/WRAPv0.9");

                service = ServiceBusService.create(config);

                int numCities = 10;  // Use as hello default, if no value is specified at command line.
                if (args.length != 0)
                {
                    if (args[0].toLowerCase().compareTo("createqueue")==0)
                    {
                        // No processing toooccur other than creating hello queue.
                        QueueInfo queueInfo = new QueueInfo("TSPQueue");

                        service.createQueue(queueInfo);

                        System.out.println("Queue named TSPQueue was created.");

                        System.exit(0);
                    }

                    if (args[0].toLowerCase().compareTo("deletequeue")==0)
                    {
                        // No processing toooccur other than deleting hello queue.
                        service.deleteQueue("TSPQueue");

                        System.out.println("Queue named TSPQueue was deleted.");

                        System.exit(0);
                    }

                    // Neither creating or deleting a queue.
                    // Assume hello value passed in is hello number of cities toosolve.
                    numCities = Integer.valueOf(args[0]);  
                }

                System.out.println("Running for " + numCities + " cities.");

                List<Integer> startCities = new ArrayList<Integer>();
                List<Integer> restCities = new ArrayList<Integer>();
                startCities.add(0);
                for(int i = 1; i<numCities; i++)
                    restCities.add(i);
                distances = new double[numCities][numCities];
                cityNames = new String[numCities];
                buildDistances("c:\\TSP\\cities.txt", numCities);
                minDistance = -1;
                bestOrder = new int[numCities];
                permutation(startCities, 0, restCities);
                System.out.println("Final solution found!");
                service.sendQueueMessage("TSPQueue", new BrokeredMessage("Complete"));
            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }
        }

    }



## <a name="how-toocreate-a-java-application-that-monitors-hello-progress-of-hello-compute-intensive-task"></a>Comment toocreate une application Java qui surveille hello la progression de la tâche de calcul intensif hello
1. Sur votre ordinateur de développement, créez une application de console Java à l’aide du code d’exemple hello à fin hello de cette section. Dans ce didacticiel, nous allons utiliser **TSPClient.java** comme nom de fichier hello Java. Comme indiqué précédemment, modifiez hello **votre\_service\_bus\_espace de noms**, **votre\_service\_bus\_propriétaire**, et **votre\_service\_bus\_clé** des espaces réservés toouse service bus **espace de noms**, **émetteur par défaut**et **clé par défaut** valeurs, respectivement.
2. Exporter hello application tooa JAR exécutable hello de package requis bibliothèques dans hello généré JAR. Dans ce didacticiel, nous allons utiliser **TSPClient.jar** comme nom de fichier JAR hello généré.

<p/>

    // TSPClient.java

    import java.util.Date;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import com.microsoft.windowsazure.services.core.*;

    public class TSPClient
    {

        public static void main(String[] args)
        {
                try
                {

                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.println("Starting at " + dateFormat.format(date) + ".");

                    String namespace = "your_service_bus_namespace";
                    String issuer = "your_service_bus_owner";
                    String key = "your_service_bus_key";

                    Configuration config;
                    config = ServiceBusConfiguration.configureWithWrapAuthentication(
                            namespace, issuer, key,
                            ".servicebus.windows.net",
                            "-sb.accesscontrol.windows.net/WRAPv0.9");

                    ServiceBusContract service = ServiceBusService.create(config);

                    BrokeredMessage message;

                    int waitMinutes = 3;  // Use as hello default, if no value is specified at command line.
                    if (args.length != 0)
                    {
                        waitMinutes = Integer.valueOf(args[0]);  
                    }

                    String waitString;

                    waitString = (waitMinutes == 1) ? "minute." : waitMinutes + " minutes.";

                    // This queue must have previously been created.
                    service.getQueue("TSPQueue");

                    int numRead;

                    String s = null;

                    while (true)
                    {

                        ReceiveQueueMessageResult resultQM = service.receiveQueueMessage("TSPQueue");
                        message = resultQM.getValue();

                        if (null != message && null != message.getMessageId())
                        {

                            // Display hello queue message.
                            byte[] b = new byte[200];

                            System.out.print("From queue: ");

                            s = null;
                            numRead = message.getBody().read(b);
                            while (-1 != numRead)
                            {
                                s = new String(b);
                                s = s.trim();
                                System.out.print(s);
                                numRead = message.getBody().read(b);
                            }
                            System.out.println();
                            if (s.compareTo("Complete") == 0)
                            {
                                // No more processing toooccur.
                                date = new Date();
                                System.out.println("Finished at " + dateFormat.format(date) + ".");
                                break;
                            }
                        }
                        else
                        {
                            // hello queue is empty.
                            System.out.println("Queue is empty. Sleeping for another " + waitString);
                            Thread.sleep(60000 * waitMinutes);
                        }
                    }

            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }

        }

    }

## <a name="how-toorun-hello-java-applications"></a>Comment toorun hello des applications Java
Exécuter des applications de calcul intensif hello, première file d’attente de hello toocreate, puis toosolve hello problème Saleseman en déplacement, qui ajoute hello meilleur itinéraire toohello service bus file d’attente actuelle. Hello lors de l’application de calcul intensif est en cours d’exécution (ou par la suite), résultats de toodisplay exécution hello client à partir de la file d’attente de bus de service hello.

### <a name="toorun-hello-compute-intensive-application"></a>application de calcul intensif hello toorun
1. Ouvrez une session sur l’ordinateur virtuel de tooyour.
2. Créez un dossier où vous exécuterez votre application. Par exemple, **C:\TSP**.
3. Copie **TSPSolver.jar** trop**c:\TSP**,
4. Créez un fichier nommé **c:\TSP\cities.txt** avec hello suivant le contenu.
   
        City_1, 1002.81, -1841.35
        City_2, -953.55, -229.6
        City_3, -1363.11, -1027.72
        City_4, -1884.47, -1616.16
        City_5, 1603.08, -1030.03
        City_6, -1555.58, 218.58
        City_7, 578.8, -12.87
        City_8, 1350.76, 77.79
        City_9, 293.36, -1820.01
        City_10, 1883.14, 1637.28
        City_11, -1271.41, -1670.5
        City_12, 1475.99, 225.35
        City_13, 1250.78, 379.98
        City_14, 1305.77, 569.75
        City_15, 230.77, 231.58
        City_16, -822.63, -544.68
        City_17, -817.54, -81.92
        City_18, 303.99, -1823.43
        City_19, 239.95, 1007.91
        City_20, -1302.92, 150.39
        City_21, -116.11, 1933.01
        City_22, 382.64, 835.09
        City_23, -580.28, 1040.04
        City_24, 205.55, -264.23
        City_25, -238.81, -576.48
        City_26, -1722.9, -909.65
        City_27, 445.22, 1427.28
        City_28, 513.17, 1828.72
        City_29, 1750.68, -1668.1
        City_30, 1705.09, -309.35
        City_31, -167.34, 1003.76
        City_32, -1162.85, -1674.33
        City_33, 1490.32, 821.04
        City_34, 1208.32, 1523.3
        City_35, 18.04, 1857.11
        City_36, 1852.46, 1647.75
        City_37, -167.44, -336.39
        City_38, 115.4, 0.2
        City_39, -66.96, 917.73
        City_40, 915.96, 474.1
        City_41, 140.03, 725.22
        City_42, -1582.68, 1608.88
        City_43, -567.51, 1253.83
        City_44, 1956.36, 830.92
        City_45, -233.38, 909.93
        City_46, -1750.45, 1940.76
        City_47, 405.81, 421.84
        City_48, 363.68, 768.21
        City_49, -120.3, -463.13
        City_50, 588.51, 679.33
5. À une invite de commandes, modifiez les répertoires tooc:\TSP.
6. Assurez-vous dossier de JRE hello bin se trouve dans la variable d’environnement PATH hello.
7. Vous aurez besoin de file d’attente du bus toocreate hello service avant d’exécuter des permutations de solveur PVC hello. Exécutez hello suivant la file d’attente de commande toocreate hello service bus.
   
        java -jar TSPSolver.jar createqueue
8. Maintenant que hello file d’attente est créée, vous pouvez exécuter des permutations de solveur PVC hello. Par exemple, exécutez hello suivant solveur de hello toorun commande 8 villes.
   
        java -jar TSPSolver.jar 8
   
   Si vous n'entrez aucun nombre, l'exécution portera sur 10 villes. Comme le solveur de hello recherche les itinéraires les plus courts en cours, il ajoute les file d’attente toohello.

> [!NOTE]
> Hello plus grande hello nombre que vous spécifiez, solveur de hello plu hello s’exécutera. Par exemple, une exécution portant sur 14 villes peut prendre quelques minutes, et une exécution portant sur 15 villes peut prendre des heures. Augmentez too16 ou davantage de villes, vous risquez de jours du runtime (finalement semaines, mois et année). Il s’agit en raison de l’augmentation rapide toohello nombre hello de permutations évaluées par le solveur de hello en tant que nombre hello de villes.
> 
> 

### <a name="how-toorun-hello-monitoring-client-application"></a>Comment toorun hello analyse de l’application client
1. Ouvrez une session sur l’ordinateur tooyour où vous allez exécuter l’application cliente de hello. Cela n’a pas besoin toobe hello même ordinateur en cours d’exécution hello **TSPSolver** application, bien qu’il peut l’être.
2. Créez un dossier où vous exécuterez votre application. Par exemple, **C:\TSP**.
3. Copie **TSPClient.jar** trop**c:\TSP**,
4. Assurez-vous dossier de JRE hello bin se trouve dans la variable d’environnement PATH hello.
5. À une invite de commandes, modifiez les répertoires tooc:\TSP.
6. Exécutez hello commande suivante.
   
        java -jar TSPClient.jar
   
    Si vous le souhaitez, spécifiez hello nombre de toosleep minutes entre la vérification de la file d’attente de hello, en passant un argument de ligne de commande. Hello période par défaut en mode veille pour la vérification de la file d’attente hello est 3 minutes, qui est utilisé si aucun argument de ligne de commande est passé trop**TSPClient**. Si vous souhaitez toouse une autre valeur pour l’intervalle de veille hello, par exemple, une minute, exécutez hello commande suivante.
   
        java -jar TSPClient.jar 1
   
    Hello client exécute jusqu'à ce qu’elle voit un message de la file d’attente de « Terminé ». Notez que si vous exécutez plusieurs occurrences de solveur de hello sans exécutant hello client, vous devrez peut-être le client de hello toorun file d’attente de plusieurs fois toocompletely hello vide. Vous pouvez également supprimer la file d’attente hello et puis recréez-le. file d’attente de toodelete hello, exécutez hello **TSPSolver** (pas **TSPClient**) commande.
   
        java -jar TSPSolver.jar deletequeue
   
    Solveur de Hello s’exécute jusqu'à ce qu’il a terminé d’examiner des tous les itinéraires.

## <a name="how-toostop-hello-java-applications"></a>Comment toostop hello des applications Java
Pour les applications clientes et les solveur de hello, vous pouvez appuyer sur **Ctrl + C** tooexit si vous souhaitez tooend toonormal préalable achèvement.

[solver_output]:media/java-run-compute-intensive-task/WA_JavaTSPSolver.png
[client_output]:media/java-run-compute-intensive-task/WA_JavaTSPClient.png
[svc_bus_node]:media/java-run-compute-intensive-task/SvcBusQueues_02_SvcBusNode.jpg
[create_namespace]:media/java-run-compute-intensive-task/SvcBusQueues_03_CreateNewSvcNamespace.jpg
[avail_namespaces]:media/java-run-compute-intensive-task/SvcBusQueues_04_SvcBusNode_AvailNamespaces.jpg
[namespace_list]:media/java-run-compute-intensive-task/SvcBusQueues_05_NamespaceList.jpg
[properties_pane]:media/java-run-compute-intensive-task/SvcBusQueues_06_PropertiesPane.jpg
[default_key]:media/java-run-compute-intensive-task/SvcBusQueues_07_DefaultKey.jpg
[add_ca_cert]: ../../../java-add-certificate-ca-store.md
