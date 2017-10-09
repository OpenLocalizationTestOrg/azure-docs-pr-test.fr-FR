---
title: "aaaUse Analytique de flux de données Azure SQL Data Warehouse | Documents Microsoft"
description: "Conseils sur l’utilisation d’Azure Stream Analytics avec Azure SQL Data Warehouse pour le développement de solutions."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 8aeb2247-20c5-4a29-b327-30a8ce09dfdc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 1278197a6764864124fd92fc672de00b83ec343f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-with-sql-data-warehouse"></a>Utiliser Azure Stream Analytics avec SQL Data Warehouse
Analytique de flux de données Azure est un service entièrement géré qui fournit le traitement des événements complexes de faible latence, hautement disponible et évolutif sur la diffusion en continu des données dans le cloud de hello. Vous pouvez principes hello en lisant [tooAzure de présentation des flux de données Analytique][Introduction tooAzure Stream Analytics]. Vous pouvez ensuite apprendre comment toocreate une solution de bout en bout avec flux de données Analytique en suivant hello [prise en main Azure flux Analytique] [ Get started using Azure Stream Analytics] didacticiel.

Dans cet article, vous allez apprendre comment toouse votre entrepôt de données SQL Azure de base de données en tant que récepteur de sortie pour vos tâches de flux Analytique.

## <a name="prerequisites"></a>Composants requis
Commencez par exécuter via hello comme suit dans hello [prise en main Azure flux Analytique] [ Get started using Azure Stream Analytics] didacticiel.  

1. Création d’une entrée de hub d’événements
2. Configuration et démarrage de l’application de génération d’événements
3. Configuration d’un travail Stream Analytics
4. Spécification d’une entrée de travail et d’une requête

Ensuite, créez une base de données SQL Data Warehouse.

## <a name="specify-job-output-azure-sql-data-warehouse-database"></a>Spécifier la sortie du travail : base de données Azure SQL Data Warehouse
### <a name="step-1"></a>Étape 1
Dans votre tâche de flux de données Analytique, cliquez sur **sortie** de haut hello de hello page, puis cliquez sur **ajouter une sortie**.

### <a name="step-2"></a>Étape 2
Sélectionnez Base de données SQL, puis cliquez sur suivant.

![][add-output]

### <a name="step-3"></a>Étape 3 :
Entrez hello valeurs suivantes sur la page suivante de hello :

* *Alias de sortie*: entrez un nom convivial pour cette sortie de travail.
* *Abonnement*:
  * Si votre base de données SQL Data Warehouse Bonjour même abonnement en tant que tâche de flux de données Analytique hello, sélectionnez de base de données SQL d’utilisation de l’abonnement actuel.
  * Si votre base de données se trouve dans un autre abonnement, sélectionnez Utiliser la base de données SQL d’un autre abonnement.
* *Base de données*: spécifiez le nom hello d’une base de données de destination.
* *Nom du serveur*: spécifiez le nom du serveur de base de données hello vous venez de spécifier hello. Vous pouvez utiliser cette toofind du portail classique Azure hello.

![][server-name]

* *Nom d’utilisateur*: spécifiez le nom d’utilisateur hello d’un compte qui dispose des autorisations d’écriture pour la base de données hello.
* *Mot de passe*: fournir un mot de passe hello pour hello de compte d’utilisateur spécifié.
* *Table*: spécifier le nom hello de la table cible hello dans la base de données hello.

![][add-database]

### <a name="step-4"></a>Étape 4
Cliquez sur tooadd de bouton de vérification hello cette tooverify qu’Analytique de flux de connexion de base de données toohello et sortie des tâches.

![][test-connection]

Lors de la base de données toohello hello connexion réussit, vous voyez une notification bas hello du portail de hello. Vous pouvez cliquer sur Tester la connexion à base de données hello bas tootest hello connexion toohello.

## <a name="next-steps"></a>Étapes suivantes
Pour une vue d’ensemble de l’intégration, consultez [Vue d’ensemble sur l’intégration de SQL Data Warehouse][SQL Data Warehouse integration overview].

Pour obtenir des conseils supplémentaires en matière de développement, consultez l’article [Vue d’ensemble sur le développement SQL Data Warehouse][SQL Data Warehouse development overview].

<!--Image references-->

[add-output]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-output.png
[server-name]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/dw-server-name.png
[add-database]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-database.png
[test-connection]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/test-connection.png

<!--Article references-->

[Introduction tooAzure Stream Analytics]: ../stream-analytics/stream-analytics-introduction.md
[Get started using Azure Stream Analytics]: ../stream-analytics/stream-analytics-real-time-fraud-detection.md
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Stream Analytics documentation]: http://azure.microsoft.com/documentation/services/stream-analytics/
