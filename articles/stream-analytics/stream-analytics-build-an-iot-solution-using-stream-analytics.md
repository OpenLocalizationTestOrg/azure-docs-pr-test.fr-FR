---
title: "aaaBuild une solution IoT à l’aide de flux de données Analytique | Documents Microsoft"
description: "Didacticiel de mise en route pour hello solution IoT Analytique de flux de données d’un scénario du guichet"
keywords: "solution IOT, fonctions de fenêtre"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: e37fc5b56c4ffc4a2d7b820afe0c17631e577ea0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-iot-solution-by-using-stream-analytics"></a>Créer une solution IoT à l’aide de Stream Analytics
## <a name="introduction"></a>Introduction
Dans ce didacticiel, vous allez apprendre comment toouse Analytique de flux de données Azure tooget en temps réel aux analyses de vos données. Les développeurs peuvent facilement combiner des flux de données, telles que les flux de clic, les journaux et les événements générés par le périphérique, avec les enregistrements historiques ou référence données tooderive gagner. En tant que service de calcul de flux en temps réel entièrement géré qui est hébergé dans Microsoft Azure, Azure flux Analytique fournit résilience intégrée, une latence faible et l’évolutivité tooget opérationnel en quelques minutes.

Après avoir effectué ce didacticiel, vous pourrez :

* Familiarisez-vous avec le portail d’Analytique de flux de données Azure hello.
* configurer et déployer un travail de diffusion en continu ;
* Expliquer les problèmes réels et de les résoudre à l’aide du langage de requête de flux de données Analytique hello.
* développer des solutions de streaming pour vos clients à l’aide de Stream Analytics en toute confiance ;
* Utilisez hello analyse et la journalisation de l’expérience tootroubleshoot problèmes.

## <a name="prerequisites"></a>Composants requis
Vous serez peut-être hello suivant toocomplete des conditions préalables ce didacticiel :

* version la plus récente de Hello [Azure PowerShell](/powershell/azure/overview)
* Visual Studio 2017, 2015, ou hello libre [Visual Studio Community](https://www.visualstudio.com/products/visual-studio-community-vs.aspx)
* Un [abonnement Azure](https://azure.microsoft.com/pricing/free-trial/)
* Privilèges d’administrateur sur l’ordinateur de hello
* Téléchargement de [TollApp.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TollApp/TollApp.zip) de hello Microsoft Download Center
* Facultatif : Code Source pour le Générateur d’événements TollApp hello dans [GitHub](https://aka.ms/azure-stream-analytics-toll-source)

## <a name="scenario-introduction-hello-toll"></a>Présentation du scénario - « Hello, Péage ! »
Une gare de péage est un dispositif très répandu. Vous rencontrez les sur les nombreuses pour les autoroutes, les ponts et les tunnels entre Bonjour. Chaque station de péage compte plusieurs guichets. À stands manuelles, vous arrêtez le service Surveillance du toopay hello péage tooan. À stands automatisés, un capteur sur chaque stand analyse une carte RFID est apposé toohello des pare-brise du véhicule que vous passez gare de péage hello. Il est le passage de hello toovisualize facile des véhicules via ces stations de péage comme un flux d’événements sur lesquels des opérations intéressantes peuvent être effectuées.

![Image de voitures à des postes de péage](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image1.jpg)

## <a name="incoming-data"></a>Données entrantes
Ce didacticiel fonctionne avec deux flux de données. Capteurs installés dans l’entrée de hello et sortie de stations de péage hello produire le premier flux de données hello. deuxième flux de Hello est un jeu de données de recherche statiques qui a des données d’inscription de véhicule.

### <a name="entry-data-stream"></a>Flux des données d’entrée
flux de données d’entrée Hello contient des informations sur les voitures lorsqu’ils entrent des stations de péage.

| TollID | EntryTime | LicensePlate | State | Make | Modèle | VehicleType | VehicleWeight | Toll | Tag |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 |2014-09-10 12:01:00.000 |JNB 7001 |NY |Honda |CRV |1 |0 |7 | |
| 1 |2014-09-10 12:02:00.000 |YXZ 1001 |NY |Toyota |Camry |1 |0 |4 |123456789 |
| 3 |2014-09-10 12:02:00.000 |ABC 1004 |CT |Ford |Taurus |1 |0 |5 |456789123 |
| 2 |2014-09-10 12:03:00.000 |XYZ 1003 |CT |Toyota |Corolla |1 |0 |4 | |
| 1 |2014-09-10 12:03:00.000 |BNJ 1007 |NY |Honda |CRV |1 |0 |5 |789123456 |
| 2 |2014-09-10 12:05:00.000 |CDE 1007 |NJ |Toyota |4x4 |1 |0 |6 |321987654 |

Voici une brève description des colonnes de hello :

| Colonne | Description |
| --- | --- |
| TollID |Hello gare de péage ID qui identifie de façon unique une gare de péage |
| EntryTime |date de Hello et l’heure de l’entrée de hello véhicule toohello gare de péage en heure UTC |
| LicensePlate |numéro de plaque Hello du véhicule de hello |
| State |État aux États-Unis |
| Marque |fabricant Hello d’automobile de hello |
| Modèle |numéro de modèle Hello d’automobile de hello |
| VehicleType |1 pour les véhicules de transport de personnes, 2 pour les véhicules commerciaux |
| WeightType |Poids du véhicule en tonnes ; 0 pour les véhicules de tourisme |
| Toll |valeur de péage Hello (USD) |
| Tag |Hello e-Tag sur automobile hello qui automatise le paiement ; vide dans laquelle le paiement de hello a été effectuée manuellement |

### <a name="exit-data-stream"></a>Flux des données de sortie
flux de données de sortie Hello contient des informations sur les voitures en laissant la station de péage hello.

| **TollId** | **ExitTime** | **LicensePlate** |
| --- | --- | --- |
| 1 |2014-09-10T12:03:00.0000000Z |JNB 7001 |
| 1 |2014-09-10T12:03:00.0000000Z |YXZ 1001 |
| 3 |2014-09-10T12:04:00.0000000Z |ABC 1004 |
| 2 |2014-09-10T12:07:00.0000000Z |XYZ 1003 |
| 1 |2014-09-10T12:08:00.0000000Z |BNJ 1007 |
| 2 |2014-09-10T12:07:00.0000000Z |CDE 1007 |

Voici une brève description des colonnes de hello :

| Colonne | Description |
| --- | --- |
| TollID |Hello gare de péage ID qui identifie de façon unique une gare de péage |
| ExitTime |date de Hello et l’heure de sortie de la récupération du véhicule hello gare de péage en heure UTC |
| LicensePlate |numéro de plaque Hello du véhicule de hello |

### <a name="commercial-vehicle-registration-data"></a>Données d’inscription des véhicules commerciaux
didacticiel de Hello utilise un instantané statique d’une base de données d’inscription de véhicule commercial.

| LicensePlate | ID d’inscription | Expiré |
| --- | --- | --- |
| SVT 6023 |285429838 |1 |
| XLZ 3463 |362715656 |0 |
| BAC 1005 |876133137 |1 |
| RIV 8632 |992711956 |0 |
| SNY 7188 |592133890 |0 |
| ELH 9896 |678427724 |1 |

Voici une brève description des colonnes de hello :

| Colonne | Description |
| --- | --- |
| LicensePlate |numéro de plaque Hello du véhicule de hello |
| ID d’inscription |ID d’inscription du véhicule Hello |
| Expiré |Hello d’état de l’inscription de véhicule de hello : 0 si l’inscription de véhicule est active, 1 si l’inscription a expiré. |

## <a name="set-up-hello-environment-for-azure-stream-analytics"></a>Définir hello environnement pour l’Analytique des flux de données Azure
toocomplete ce didacticiel, vous avez besoin d’un abonnement Microsoft Azure. Microsoft propose un essai gratuit des services Microsoft Azure.

Si vous n’avez pas de compte Azure, vous pouvez [demander un essai gratuit](http://azure.microsoft.com/pricing/free-trial/).

> [!NOTE]
> toosign pour un essai gratuit, vous devez un appareil mobile qui peut recevoir des messages texte et une carte de crédit.
> 
> 

Veillez à toofollow hello les étapes de section de « Nettoyage de votre compte Azure » hello à fin hello de cet article afin que vous pouvez utiliser hello mieux votre crédit Azure.

## <a name="provision-azure-resources-required-for-hello-tutorial"></a>Prévoir des ressources Azure requises pour le didacticiel de hello
Ce didacticiel requiert deux tooreceive de concentrateurs d’événements *entrée* et *quitter* des flux de données. Base de données SQL Azure génère des résultats de hello des tâches de flux de données Analytique hello. Stockage Azure stocke les données de référence sur les inscriptions de véhicules.

Vous pouvez utiliser hello Setup.ps1 script dans le dossier de TollApp hello sur GitHub toocreate toutes les ressources requises. Intérêt hello de temps, nous vous recommandons de faire. Si vous souhaitez que toolearn plus en détail comment tooconfigure ces ressources Bonjour portail Azure, consultez l’annexe « Configuration des ressources de didacticiel dans le portail Azure » de toohello.

Téléchargez et enregistrez la prise en charge de hello [TollApp](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TollApp/TollApp.zip) dossier et les fichiers.

Ouvrez une fenêtre **Microsoft Azure PowerShell***en tant qu’administrateur*. Si vous n’avez pas encore d’Azure PowerShell, suivez les instructions de hello dans [installer et configurer Azure PowerShell](/powershell/azure/overview) tooinstall il.

Étant donné que Windows empêche automatiquement les fichiers .exe, .dll et .ps1, vous devez stratégie d’exécution hello tooset avant d’exécuter les script hello. Assurez-vous que la fenêtre d’Azure PowerShell hello est en cours d’exécution *en tant qu’administrateur*. Exécutez l’applet de commande **Set-ExecutionPolicy unrestricted**. Quand vous y êtes invité, tapez **O**.

![Capture d’écran de l’applet de commande « Set-ExecutionPolicy illimité » en cours d’exécution dans la fenêtre Azure PowerShell](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image2.png)

Exécutez **Get-ExecutionPolicy** toomake assurer du fonctionnait de la commande hello.

![Capture d’écran de l’applet de commande « Get-ExecutionPolicy » en cours d’exécution dans la fenêtre Azure PowerShell](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image3.png)

Accédez répertoire toohello qui contient les scripts hello et application du générateur.

![Capture d’écran de « cd .\TollApp\TollApp « en cours d’exécution dans la fenêtre Azure PowerShell de hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image4.png)

Type **.\\ Setup.ps1** tooset votre compte Azure, créer et configurer toutes les ressources requises et démarrer les événements toogenerate. script de Hello choisit de façon aléatoire d’une région toocreate vos ressources. tooexplicitly spécifier une région, vous pouvez passer hello **-emplacement** paramètre comme hello l’exemple suivant :

**.\\Setup.ps1 -location “Central US”**

![Capture d’écran de la page de hello signe dans Azure](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image5.png)

script de Hello ouvre hello **connexion** page pour Microsoft Azure. Entrez les informations d’identification de votre compte.

> [!NOTE]
> Si votre compte a accès toomultiple abonnements, vous serez le nom de l’abonnement hello tooenter fréquentes que vous souhaitez toouse pour le didacticiel de hello.
> 
> 

script de Hello peut prendre plusieurs minutes toorun. Une fois celle-ci terminée, sortie de hello doit ressembler à hello suivant capture d’écran.

![Capture d’écran de sortie du script de hello dans la fenêtre Azure PowerShell de hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image6.PNG)

Vous verrez également une autre fenêtre est similaire toohello suivant capture d’écran. Cette application envoie des événements de concentrateurs d’événements tooAzure, qui est le didacticiel de hello toorun requis. Par conséquent, n’arrêtez l’application hello ou fermez cette fenêtre jusqu'à ce que vous avez terminé le didacticiel de hello.

![Capture d’écran « Envoi de données de hub d’événements »](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image7.png)

Vous doit être en mesure de toosee vos ressources dans le portail Azure maintenant. Accédez trop<https://portal.azure.com>et connectez-vous avec vos informations d’identification de compte. Notez que certaines fonctionnalités utilisant actuellement portail classique de hello. Ces étapes sont clairement indiquées.

### <a name="azure-event-hubs"></a>Hubs d'événements Azure
Bonjour portail Azure, cliquez sur **davantage de services** bas hello du volet de gauche de gestion hello. Type **concentrateurs d’événements** hello champ fourni et cliquez sur **concentrateurs d’événements**. Cette action lance un nouveau toodisplay Bonjour de navigateur fenêtre **SERVICE BUS** zone Bonjour **portail classic**. Ici, vous pouvez voir hello concentrateur d’événements créés par hello Setup.ps1 script.

![Service Bus](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image8.png)

Cliquez sur hello qui commence par *tolldata*. Cliquez sur hello **concentrateurs d’événements** onglet. Deux concentrateurs d’événements nommés *entry* et *exit* apparaissent dans cet espace de noms.

![Onglet de concentrateurs d’événements dans le portail classique de hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image9.png)

### <a name="azure-storage-container"></a>Conteneur Azure Storage
1. Revenir en arrière onglet toohello dans votre portail ouvert tooAzure de navigateur. Cliquez sur **stockage** sur hello à gauche de conteneur de stockage Azure hello toosee portail Azure hello qui est utilisé dans le didacticiel de hello.
   
    ![Élément de menu de stockage](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image11.png)
2. Cliquez sur hello qui commencent par *tolldata*. Cliquez sur hello **conteneurs** conteneur d’onglet toosee hello créé.
   
    ![Onglet conteneurs Bonjour portail Azure](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image10.png)
3. Cliquez sur hello **tolldata** hello toosee de conteneur téléchargé le fichier JSON qui comporte des données d’inscription de véhicule.
   
    ![Capture d’écran du fichier de registration.json hello dans le conteneur de hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image12.png)

### <a name="azure-sql-database"></a>Base de données SQL Azure
1. Revenir en arrière toohello portail Azure sur hello premier onglet qui a été ouvert dans le navigateur de hello. Cliquez sur **bases de données SQL** sur hello à gauche de hello toosee portail Azure hello base de données SQL qui sera utilisé dans le didacticiel de hello et cliquez sur **tolldatadb**.
   
    ![Capture d’écran de hello créé la base de données SQL](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image15.png)
2. Nom du serveur hello copie sans numéro de port hello (*nom_serveur*. database.windows.net, par exemple).
    ![Capture d’écran de hello créé la base de données de base de données SQL](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image15a.png)

## <a name="connect-toohello-database-from-visual-studio"></a>Se connecter toohello de base de données à partir de Visual Studio
Utilisez les résultats de la requête tooaccess Visual Studio dans la base de données de sortie hello.

Connexion de base de données SQL toohello (destination hello) à partir de Visual Studio :

1. Ouvrez Visual Studio, puis cliquez sur **outils** > **connecter tooDatabase**.
2. Si vous y êtes invité, sélectionnez la source de données **Microsoft SQL Server** .
   
    ![Boîte de dialogue Modifier la source de données](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image16.png)
3. Bonjour **nom du serveur** champ, collez le nom que vous avez copié dans la section précédente de hello de hello portail Azure hello (autrement dit, *nom_serveur*. database.windows.net).
4. Cliquez sur **Utiliser l’authentification SQL Server**.
5. Entrez **tolladmin** Bonjour **nom d’utilisateur** champ et **123toll !** Bonjour **mot de passe** champ.
6. Cliquez sur **sélectionner ou entrer un nom de base de données**, puis sélectionnez **TollDataDB** en tant que base de données hello.
   
    ![Boîte de dialogue Ajouter une connexion](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image17.jpg)
7. Cliquez sur **OK**.
8. Ouvrez l’Explorateur de serveurs.
   
    ![Explorateur de serveurs](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image18.png)
9. Consultez les quatre tables de base de données TollDataDB hello.
   
    ![Tables de base de données TollDataDB hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image19.jpg)

## <a name="event-generator-tollapp-sample-project"></a>Générateur d’événements - Exemple de projet TollApp
Hello script PowerShell démarre automatiquement toosend événements à l’aide du programme d’application exemple hello TollApp. Vous n’avez pas besoin tooperform les éventuelles étapes supplémentaires.

Toutefois, si vous souhaitez dans les détails d’implémentation, vous pouvez trouver le code de source de hello Hello TollApp application dans GitHub [exemples/TollApp](https://aka.ms/azure-stream-analytics-toll-source).

![Capture d’écran d’exemple de code affiché dans Visual Studio](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image20.png)

## <a name="create-a-stream-analytics-job"></a>Création d’un travail Stream Analytics
1. Bonjour portail Azure, cliquez sur hello signe plus dans l’angle supérieur gauche de hello de hello page toocreate une nouvelle tâche de flux de données Analytique. Sélectionnez **Intelligence + analyse**, puis cliquez sur **Tâche Stream Analytics**.
   
    ![Bouton Nouveau](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image21.png)
2. Fournissez un nom de travail, valider l’abonnement de hello est correct et ensuite créer un nouveau groupe de ressources Bonjour même région que hello stockage concentrateur d’événements (valeur par défaut est Amérique du Sud pour hello script).
3. Cliquez sur **code confidentiel toodashboard** , puis **créer** bas hello de page de hello.
   
    ![Option Créer une tâche Stream Analytics](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image22.png)

## <a name="define-input-sources"></a>Définir les sources d’entrée
1. travail de Hello crée et ouvre la page du travail hello. Ou vous pouvez cliquer sur hello créé le travail de l’analytique sur le tableau de bord de portail hello.

2. Cliquez sur hello **entrées** onglet source de données toodefine hello.
   
    ![onglet d’entrées Hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image24.png)
3. Cliquez sur **AJOUTER UNE ENTRÉE**.
   
    ![Ajouter une entrée de Hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image25.png)
4. Tapez **EntryStream** comme **ALIAS D’ENTRÉE**.
5. Le Type de source est **Flux de données**.
6. La Source est **Event Hub**.
7. **Espace de noms service bus** doit être hello TollData un Bonjour liste déroulante.
8. **Nom de hub d’événements** doit être défini trop**entrée**.
9. **Nom de la stratégie hub événement*est **RootManageSharedAccessKey** (valeur par défaut de hello).
10. Sélectionnez **JSON** pour l’option **Format de sérialisation de l’événement**, et **UTF8** pour **Encodage**.
   
    Vos paramètres ressemblent à ceci :
   
    ![Paramètres de hub d’événements](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image28.png)

10. Cliquez sur **créer** bas hello d’Assistant de hello page toofinish hello.
    
    Maintenant que vous avez créé des flux d’entrée hello, vous suivrez hello même flux de sortie hello toocreate étapes. Être vraiment tooenter valeurs comme sur hello suivant capture d’écran.
    
    ![Paramètres de flux de sortie hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image31.png)
    
    Vous avez défini deux flux d’entrée :
    
    ![Flux d’entrée définis dans hello portail Azure](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image32.png)
    
    Ensuite, vous allez ajouter des entrées de données de référence pour le fichier blob hello qui contient les données d’inscription de voiture.
11. Cliquez sur **ajouter**, puis suivez hello même processus pour les entrées de flux hello mais sélectionnez **les données de référence** au lieu de **flux de données** et hello **Alias d’entrée**  est **inscription**.

12. Compte de stockage commençant par **tolldata**. nom du conteneur Hello doit être **tolldata**et hello **modèle de chemin d’accès** doit être **registration.json**. Ce nom de fichier respecte la casse et doit être en **minuscules**.
    
    ![Paramètres de stockage d’objets blob](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image34.png)
13. Cliquez sur **créer** Assistant de hello toofinish.

Désormais, toutes les entrées sont définies.

## <a name="define-output"></a>Définir la sortie
1. Sur le volet de présentation du travail hello Analytique de flux de données, sélectionnez **sorties**.
   
    ![onglet sortie de Hello et l’option « Ajouter une sortie »](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image37.png)
2. Cliquez sur **Add**.
3. Ensemble hello **alias de sortie** too'output », puis **récepteur** trop**base de données SQL**.
3. Sélectionnez le nom du serveur hello qui a été utilisé dans la section « TooDatabase de se connecter à partir de Visual Studio » de l’article de hello de hello. nom de base de données Hello est **TollDataDB**.
4. Entrez **tolladmin** Bonjour **nom d’utilisateur** champ, **123toll !** Bonjour **mot de passe** champ, et **TollDataRefJoin** Bonjour **TABLE** champ.
   
    ![Paramètres SQL Database](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image38.png)
5. Cliquez sur **Create**.

## <a name="azure-stream-analytics-query"></a>Requête Azure Stream Analytics
Hello **requête** onglet contient une requête SQL que transformations hello les données entrantes.

![Onglet de requête toohello été ajouté à une requête](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image39.png)

Ce didacticiel tentatives tooanswer plusieurs questions liées tootoll données et constructions de flux de données Analytique des requêtes qui peuvent être utilisées dans Azure flux Analytique tooprovide une réponse appropriée.

Avant de commencer votre premier travail Analytique des flux de données, examinons quelques scénarios et syntaxe de requête hello.

## <a name="introduction-tooazure-stream-analytics-query-language"></a>Introduction tooAzure langage de requête Analytique de flux de données
- - -
Supposons que vous devez toocount hello de véhicules qui permet d’entrer une gare de péage. Comme il s’agit d’un flux continu d’événements, vous avez toodefine une « période de temps. » Nous allons modifier hello toobe de question « Combien de véhicules permet d’entrer une gare de péage toutes les trois minutes ? ». Il s’agit de hello tooas communément référence bascule count.

Examinons la requête Analytique de flux de données Azure hello qui répond à cette question :

    SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count
    FROM EntryStream TIMESTAMP BY EntryTime
    GROUP BY TUMBLINGWINDOW(minute, 3), TollId

Comme vous pouvez le voir, Analytique de flux de données Azure utilise un langage de requête tel que SQL et ajoute quelques extensions toospecify liées au temps aspects de hello requête.

Pour plus d’informations, consultez [gestion du temps](https://msdn.microsoft.com/library/azure/mt582045.aspx) et [fenêtrage](https://msdn.microsoft.com/library/azure/dn835019.aspx) constructions utilisées dans la requête hello à partir de MSDN.

## <a name="testing-azure-stream-analytics-queries"></a>Test des requêtes Azure Stream Analytics
Maintenant que vous avez écrit votre première requête Analytique de flux de données Azure, il est tootest de temps à l’aide de fichiers de données exemple situé dans votre dossier de TollApp Bonjour suivant le chemin d’accès :

**..\\TollApp\\TollApp\\Data**

Ce dossier contient les fichiers suivants de hello :

* Entry.json
* Exit.json
* registration.json

## <a name="question-1-number-of-vehicles-entering-a-toll-booth"></a>Question 1 : Nombre de véhicules arrivant à un poste de péage
1. Ouvrez hello portail Azure et accédez tooyour créé Analytique de flux de données Azure travail. Cliquez sur hello **requête** onglet et collez la requête à partir de la section précédente de hello.

2. toovalidate cette requête sur les données d’exemple, téléchargement des données de hello en hello entrée EntryStream en cliquant sur hello... symbole et en sélectionnant **télécharger des exemples de données à partir du fichier**.

    ![Capture d’écran du fichier de Entry.json hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image41.png)
3. Dans le volet hello qui s’affiche le fichier hello select (Entry.json) sur votre ordinateur local cliquez sur **OK**. Hello **Test** icône sera désormais éclairer et être interactif.
   
    ![Capture d’écran du fichier de Entry.json hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image42.png)
3. Valider sortie hello de requête de hello comme prévu :
   
    ![Résultats des tests de hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image43.png)

## <a name="question-2-report-total-time-for-each-car-toopass-through-hello-toll-booth"></a>Question 2 : Durée totale de chaque toopass voiture gare de péage hello par le biais de rapports
temps moyen Hello requise pour un toopass voiture via gare de hello permet l’efficacité de hello tooassess du processus de hello et expérience du client hello.

durée totale de hello toofind, il faut toojoin hello EntryTime flux avec flux de ExitTime hello. Vous permet de joindre les flux hello sur des colonnes TollId et LicencePlate. Hello **joindre** opérateur nécessite que vous toospecify manœuvre temporelle qui décrit la différence entre hello joint des événements de temps acceptable hello. Vous allez utiliser **DATEDIFF** fonction toospecify que les événements doivent être pas plus de 15 minutes entre eux. Vous allez également appliquer hello **DATEDIFF** tooexit de fonction et entrée heures toocompute hello temps réel une voiture est occupé Bonjour payant station. Notez la différence hello d’utilisation hello de **DATEDIFF** lorsqu’il est utilisé dans un **sélectionnez** instruction plutôt qu’un **joindre** condition.

    SELECT EntryStream.TollId, EntryStream.EntryTime, ExitStream.ExitTime, EntryStream.LicensePlate, DATEDIFF (minute , EntryStream.EntryTime, ExitStream.ExitTime) AS DurationInMinutes
    FROM EntryStream TIMESTAMP BY EntryTime
    JOIN ExitStream TIMESTAMP BY ExitTime
    ON (EntryStream.TollId= ExitStream.TollId AND EntryStream.LicensePlate = ExitStream.LicensePlate)
    AND DATEDIFF (minute, EntryStream, ExitStream ) BETWEEN 0 AND 15

1. tootest cette requête, requête hello de mise à jour sur hello **requête** pour le travail de hello. Ajouter le fichier de test hello pour **ExitStream** comme **EntryStream** a été entré précédemment.
   
2. Cliquez sur **Test**.

3. Sélectionnez hello case tootest hello requêtes et vues hello sortie :
   
    ![Sortie de test de hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image45.png)

## <a name="question-3-report-all-commercial-vehicles-with-expired-registration"></a>Question 3 : Signaler tous les véhicules commerciaux dont l’inscription a expiré
Analytique de flux de données Azure peuvent utiliser des instantanés statiques des données toojoin avec des flux de données temporelles. toodemonstrate cette fonctionnalité, hello utilisation suivant l’exemple de question.

Si un véhicule commercial est inscrit auprès d’un péage hello, il peut traverser gare de péage hello sans être arrêté pour inspection. Vous allez utiliser tooidentify de table de recherche d’inscription de véhicule Commercial de tous les véhicules commerciaux qui ont expiré des enregistrements.

```
SELECT EntryStream.EntryTime, EntryStream.LicensePlate, EntryStream.TollId, Registration.RegistrationId
FROM EntryStream TIMESTAMP BY EntryTime
JOIN Registration
ON EntryStream.LicensePlate = Registration.LicensePlate
WHERE Registration.Expired = '1'
```

tootest une requête à l’aide de données de référence, vous devez toodefine une source d’entrée pour les données de référence hello, qui est déjà fait.

tootest cette requête, collez les requêtes de hello en hello **requête** , cliquez sur **Test**et spécifiez l’inscription de hello sources d’entrée de hello deux exemples de données et cliquez sur **Test**.  
   
![Sortie de test de hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image46.png)

## <a name="start-hello-stream-analytics-job"></a>Démarrer la tâche de flux de données Analytique hello
Il est maintenant temps toofinish hello configuration et démarrage hello travail. Enregistrer la requête de hello de Question 3, ce qui produira un résultat que correspondances hello schéma Hello **TollDataRefJoin** table de sortie.

Accédez toohello travail **tableau de bord**, puis cliquez sur **Démarrer**.

![Capture d’écran du bouton Démarrer de hello dans le tableau de bord projet hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image48.png)

Dans la boîte de dialogue hello qui s’ouvre, modifiez hello **démarrer une sortie** trop de temps**heure personnalisé**. Modification hello heure tooone heure avant hello heure actuelle. Cette modification garantit que tous les événements à partir du concentrateur d’événements hello sont traitées depuis le démarrage d’événements de hello toogenerate au début de hello du didacticiel de hello. Cliquez maintenant sur hello **Démarrer** travail de bouton toostart hello.

![Sélection de Heure personnalisée](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image49.png)

Démarrage de la tâche hello peut prendre quelques minutes. Vous pouvez voir l’état de hello sur la page de niveau supérieur hello pour les flux de données Analytique.

![Capture d’écran de l’état de hello du travail de hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image50.png)

## <a name="check-results-in-visual-studio"></a>Vérifier les résultats dans Visual Studio
1. Ouvrez l’Explorateur de serveurs Visual Studio et avec le bouton droit hello **TollDataRefJoin** table.
2. Cliquez sur **afficher les données de Table** sortie de hello toosee de votre travail.
   
    ![Sélection de « Afficher les données de la table » dans l’Explorateur de serveurs](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image51.jpg)

## <a name="scale-out-azure-stream-analytics-jobs"></a>Mettre à l’échelle des tâches Azure Stream Analytics
Analytique de flux de données Azure est conçu tooelastically l’échelle afin qu’il puisse gérer une grande quantité de données. la requête Analytique de flux de données Azure Hello peut utiliser un **PARTITION BY** clause tootell hello système que cette étape sera montée en charge. **PartitionId** est une colonne spéciale qui hello système ajoute l’ID de partition hello toomatch d’entrée de hello (concentrateur d’événements).

    SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*)AS Count
    FROM EntryStream TIMESTAMP BY EntryTime PARTITION BY PartitionId
    GROUP BY TUMBLINGWINDOW(minute,3), TollId, PartitionId

1. Tâche en cours d’arrêt hello, requête hello de mise à jour Bonjour **requête** onglet et ouvrez hello **paramètres** ENGRENAGE dans le tableau de bord projet hello. Cliquez sur **Scale**.
   
    **UNITÉS de diffusion en continu** Définir montant hello de puissance de calcul qui hello travail peut recevoir.
2. Modification hello déroulante à partir de 1 à 6.
   
    ![Capture d’écran de la sélection de 6 unités de diffusion en continu](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image52.png)
3. Accédez toohello **sorties** onglet et renommez hello du tableau SQL hello trop**TollDataTumblingCountPartitioned**.

Maintenant, si vous démarrez le travail de hello Analytique de flux de données Azure peut distribuer le travail sur plusieurs ressources de calcul et obtenir un meilleur débit. Veuillez noter que hello TollApp application envoie également des événements partitionnées par TollId.

## <a name="monitor"></a>Surveiller
Hello **moniteur** zone contient des statistiques sur hello travail en cours d’exécution. Première configuration est nécessaire de compte de stockage toouse hello Bonjour même région (nom de l’appel comme reste hello de ce document).   

![Capture d’écran de la surveillance](media/stream-analytics-build-an-iot-solution-using-stream-analytics/monitoring.png)

Vous pouvez accéder aux **journaux d’activité** à partir du tableau de bord projet hello **paramètres** zone également.


## <a name="conclusion"></a>Conclusion
Ce didacticiel introduit le service de Azure flux Analytique toohello. Il a montré comment tooconfigure entrées et sorties pour hello la tâche de flux de données Analytique. À l’aide du scénario de péage données hello, didacticiel de hello expliqué types courants de problèmes qui surviennent dans un espace de données de mouvement et comment ils peuvent être résolus avec des requêtes de type SQL simples dans Azure flux Analytique hello. didacticiel de Hello décrit les constructions d’extension SQL pour l’utilisation des données temporelles. Il a montré comment toojoin flux de données, mode de fonctionnement du flux de données de hello tooenrich avec les données de référence statiques et tooscale à un débit plus élevé de tooachieve de requête.

Bien que ce didacticiel constitue une bonne introduction, il n’est en aucun cas complet. Vous trouverez plusieurs modèles de requête à l’aide de la langue SAQL hello sur [exemples pour les modèles d’utilisation courants Analytique de flux de requête](stream-analytics-stream-analytics-query-patterns.md).
Consultez toohello [documentation en ligne](https://azure.microsoft.com/documentation/services/stream-analytics/) toolearn plus Analytique de flux de données Azure.

## <a name="clean-up-your-azure-account"></a>Nettoyer votre compte Azure
1. Arrêter la tâche de flux de données Analytique hello Bonjour portail Azure.
   
    Hello Setup.ps1 script crée deux concentrateurs d’événements et une base de données SQL. Hello suivant l’aide des instructions que vous nettoyez les ressources à fin hello du didacticiel de hello.
2. Dans une fenêtre PowerShell, tapez **.\\ CleanUp.ps1** script hello toostart qui supprime les ressources utilisées dans le didacticiel de hello.
   
   > [!NOTE]
   > Les ressources sont identifiées par nom de hello. Assurez-vous de vérifier attentivement chaque élément avant d’en confirmer la suppression.
   > 
   > 


