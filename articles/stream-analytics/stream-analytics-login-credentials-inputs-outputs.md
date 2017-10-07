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
# <a name="rotate-login-credentials-for-inputs-and-outputs-in-stream-analytics-jobs"></a>Rotation des informations d'identification pour les entrées et les sorties dans des travaux Stream Analytics
## <a name="abstract"></a>Résumé
Analytique de flux de données Azure aujourd'hui n’autorise pas remplacer les informations d’identification hello sur une entrée/sortie pendant l’exécution du travail de hello.

Analytique de flux de données Azure ne prend pas en charge la reprise d’une tâche à partir de la dernière sortie, nous voulions processus tooshare hello pour minimiser le retard hello entre hello l’arrêt et démarrage du travail de hello et faire pivoter les informations d’identification de connexion hello.

## <a name="part-1---prepare-hello-new-set-of-credentials"></a>Partie 1 : préparer les hello nouvel ensemble d’informations d’identification :
Cette partie est applicable toohello suivant des entrées/sorties :

* Stockage d’objets blob
* Hubs d'événements
* Base de données SQL
* Stockage de tables

Pour les autres entrées/sorties, passez à la partie 2.

### <a name="blob-storagetable-storage"></a>Stockage d’objets blob/de tables
1. Consulter l’extension du stockage toohello le portail de gestion Azure hello :  
   ![graphic1][graphic1]
2. Recherchez stockage hello utilisé par votre travail et allez dans celui-ci :  
   ![graphic2][graphic2]
3. Cliquez sur commande de gérer les clés d’accès hello :  
   ![graphic3][graphic3]
4. Entre hello clé d’accès primaire et hello clé d’accès secondaire, **pick hello ne pas utilisé par votre travail**.
5. Appuyez sur Régénérer :   
   ![graphic4][graphic4]
6. Copiez la clé de hello qui vient d’être généré :  
   ![graphic5][graphic5]
7. Continuer tooPart 2.

### <a name="event-hubs"></a>Hubs d'événements
1. Atteindre l’extension de Service Bus toohello sur le portail de gestion Azure hello :  
   ![graphic6][graphic6]
2. Recherchez hello Namespace de Bus de Service utilisé par votre tâche et allez dans celui-ci :  
   ![graphic7][graphic7]
3. Si votre projet utilise une stratégie d’accès partagé sur hello Namespace de Bus de Service, passer toostep 6  
4. Consultez l’onglet de concentrateurs d’événements toohello :  
   ![graphic8][graphic8]
5. Recherchez hello concentrateur d’événements utilisée par votre travail et allez dans celui-ci :  
   ![graphic9][graphic9]
6. Accédez toohello onglet Configurer :  
   ![graphic10][graphic10]
7. Hello déroulante Nom de la stratégie, recherchez la stratégie d’accès hello partagé utilisée par votre projet :  
   ![graphic11][graphic11]
8. Entre hello Primary Key et hello clé secondaire, **pick hello ne pas utilisé par votre travail**.  
9. Appuyez sur Régénérer :   
   ![graphic12][graphic12]
10. Copiez la clé de hello qui vient d’être généré :  
   ![graphic13][graphic13]
11. Continuer tooPart 2.  

### <a name="sql-database"></a>Base de données SQL
> [!NOTE]
> Remarque : vous devrez tooconnect toohello Service de base de données SQL. Nous allons tooshow comment toodo à l’aide de cette hello expérience de gestion sur hello portail de gestion Azure, mais vous pouvez choisir toouse un outil côté client telles que SQL Server Management Studio.
>
> 

1. Consulter le portail de gestion Azure hello extension des bases de données SQL toohello :  
   ![graphic14][graphic14]
2. Recherchez hello utilisée par votre travail de la base de données SQL et **cliquez sur le serveur de hello** lier sur hello même ligne :  
   ![graphic15][graphic15]
3. Cliquez sur hello gérer commande :  
   ![graphic16][graphic16]
4. Tapez Base de données principale :   
   ![graphic17][graphic17]
5. Tapez votre nom d’utilisateur, votre mot de passe, puis cliquez sur Ouvrir une session :   
   ![graphic18][graphic18]
6. Cliquez sur Nouvelle requête :   
   ![graphic19][graphic19]
7. Type Bonjour suivant la requête en remplaçant < login_name > avec votre nom d’utilisateur et le remplacement <enterStrongPasswordHere> avec votre nouveau mot de passe :  
   `CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'`
8. Cliquez sur Exécuter :   
   ![graphic20][graphic20]
9. Revenir en arrière toostep 2 et cette fois, cliquez sur base de données hello :  
   ![graphic21][graphic21]
10. Cliquez sur hello gérer commande :  
   ![graphic22][graphic22]
11. Tapez votre nom d’utilisateur, votre mot de passe, puis cliquez sur Ouvrir une session :   
   ![graphic23][graphic23]
12. Cliquez sur Nouvelle requête :   
   ![graphic24][graphic24]
13. Tapez Bonjour suivant la requête en remplaçant < nom_utilisateur > avec un nom en fonction duquel vous voulez tooidentify cette connexion dans le contexte de hello de cette base de données (vous pouvez fournir hello la même valeur que vous avez attribué < login_name >, par exemple) et en remplaçant < login_name > par votre nouveau nom d’utilisateur :  
   `CREATE USER <user_name> FROM LOGIN <login_name>`
14. Cliquez sur Exécuter :   
   ![graphic25][graphic25]
15. Vous devez maintenant fournir votre nouvel utilisateur hello mêmes rôles et les privilèges votre utilisateur d’origine.
16. Continuer tooPart 2.

## <a name="part-2-stopping-hello-stream-analytics-job"></a>Partie 2 : Arrêt hello tâche Analytique de flux de données
1. Consulter le portail de gestion Azure hello extension du flux de données Analytique toohello :  
   ![graphic26][graphic26]
2. Recherchez votre travail et accédez-y :   
   ![graphic27][graphic27]
3. Accédez toohello entrées onglet ou hello sorties selon si vous faites pivoter les informations d’identification hello sur une entrée ou une sortie.  
   ![graphic28][graphic28]
4. Cliquez sur la commande d’arrêt hello et vérifiez le travail de hello s’est arrêté :  
   ![graphic29][graphic29] attendre hello travail toostop.
5. Recherchez hello d’entrée/sortie souhaité informations d’identification toorotate active et accédez dans celui-ci :  
   ![graphic30][graphic30]
6. Continuer tooPart 3.

## <a name="part-3-editing-hello-credentials-on-hello-stream-analytics-job"></a>Partie 3 : Modification hello informations d’identification sur hello tâche Analytique de flux de données
### <a name="blob-storagetable-storage"></a>Stockage d’objets blob/de tables
1. Rechercher le champ de clé de compte de stockage hello et collez votre clé qui vient d’être générée :  
   ![graphic31][graphic31]
2. Cliquez sur la commande hello et confirmer l’enregistrement de vos modifications :  
   ![graphic32][graphic32]
3. Un test de connexion démarre automatiquement lorsque vous enregistrez vos modifications ; assurez-vous qu’il a réussi.
4. Continuer tooPart 4.

### <a name="event-hubs"></a>Hubs d'événements
1. Rechercher le champ de clé stratégie Hub d’événements hello et collez votre clé qui vient d’être générée :  
   ![graphic33][graphic33]
2. Cliquez sur la commande hello et confirmer l’enregistrement de vos modifications :  
   ![graphic34][graphic34]
3. Un test de connexion démarre automatiquement lorsque vous enregistrez vos modifications ; assurez-vous qu’il a réussi.
4. Continuer tooPart 4.

### <a name="power-bi"></a>Power BI
1. Cliquez sur l’autorisation de renouveler hello :  

   ![graphic35][graphic35]
2. Vous obtiendrez hello après confirmation :  

   ![graphic36][graphic36]
3. Cliquez sur la commande hello et confirmer l’enregistrement de vos modifications :  
   ![graphic37][graphic37]
4. Un test de connexion démarre automatiquement lorsque vous enregistrez vos modifications ; assurez-vous qu’il a réussi.
5. Continuer tooPart 4.

### <a name="sql-database"></a>Base de données SQL
1. Recherche des champs de nom d’utilisateur et mot de passe hello et collez votre nouveau jeu créé des informations d’identification :  
   ![graphic38][graphic38]
2. Cliquez sur la commande hello et confirmer l’enregistrement de vos modifications :  
   ![graphic39][graphic39]
3. Un test de connexion démarre automatiquement lorsque vous enregistrez vos modifications ; assurez-vous qu’il a réussi.  
4. Continuer tooPart 4.

## <a name="part-4-starting-your-job-from-last-stopped-time"></a>Partie 4 – Démarrage de votre travail à partir de l’heure du dernier arrêt
1. Quittez hello d’entrée/sortie :  
   ![graphic40][graphic40]
2. Cliquez sur commande de démarrage hello :  
   ![graphic41][graphic41]
3. Choisir l’heure du dernier arrêt de hello et cliquez sur OK :  
   ![graphic42][graphic42]
4. Continuer tooPart 5.  

## <a name="part-5-removing-hello-old-set-of-credentials"></a>Partie 5 : Suppression hello ancien jeu d’informations d’identification
Cette partie est applicable toohello suivant des entrées/sorties :

* Stockage d’objets blob
* Hubs d'événements
* Base de données SQL
* Stockage de tables

### <a name="blob-storagetable-storage"></a>Stockage d’objets blob/de tables
Répétez partie 1 pour hello clé d’accès qui était utilisé précédemment par votre tâche toorenew hello désormais inutilisée clé d’accès.

### <a name="event-hubs"></a>Hubs d'événements
Répétez partie 1 pour hello clé qui était utilisé précédemment par votre tâche toorenew hello clé maintenant inutilisé.

### <a name="sql-database"></a>Base de données SQL
1. Revenir en arrière fenêtre de requête toohello à partir de la partie 1 étape 7 et tapez Bonjour suivant la requête, en remplaçant < previous_login_name > par nom d’utilisateur qui a été utilisé précédemment par votre tâche de hello :  
   `DROP LOGIN <previous_login_name>`  
2. Cliquez sur Exécuter :   
   ![graphic43][graphic43]  

Vous devez obtenir hello après confirmation : 

    Command(s) completed successfully.

## <a name="get-help"></a>Obtenir de l’aide
Pour obtenir une assistance, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Étapes suivantes
* [Introduction tooAzure Analytique de flux de données](stream-analytics-introduction.md)
* [Prise en main d’Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l'échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Références sur le langage des requêtes d'Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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

