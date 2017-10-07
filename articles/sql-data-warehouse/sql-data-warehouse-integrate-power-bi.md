---
title: "aaaUse Power BI avec l’entrepôt de données SQL | Documents Microsoft"
description: "Conseils relatifs à l’utilisation de Power BI avec Azure SQL Data Warehouse pour le développement de solutions."
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: b12bee87-2268-40c2-81bf-ab27588b32e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: a3a347493d07af6824a561567f05894cfe3c0471
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-with-sql-data-warehouse"></a>Utiliser Power BI avec SQL Data Warehouse
Comme avec la base de données SQL Azure, entrepôt de données du SQL directe Connect permet utilisateur tooleverage puissante logique poussée vers le bas en même temps que les fonctions d’analyse hello de Power BI.  Avec la connexion directe, requêtes sont envoyées tooyour arrière Azure SQL Data Warehouse en temps réel que vous explorez les données hello.  Ceci, combiné avec échelle hello SQL Data Warehouse, permet aux utilisateurs des rapports dynamiques toocreate en minutes par rapport à plusieurs téraoctets de données.  En outre, introduction hello Hello ouvrir du bouton Power BI permet aux utilisateurs toodirectly se connecter à Power BI tootheir SQL Data Warehouse sans recueillir des informations à partir d’autres parties de Azure.

Lorsque vous utilisez la connexion directe, notez les points suivants :

* Spécifiez le nom du serveur complet hello lors de la connexion (voir ci-dessous pour plus de détails)
* Que les règles de pare-feu de base de données hello sont configurés trop « autorisent l’accès tooAzure services ».
* Toutes les actions telles que la sélection d’une colonne ou l’ajout d’un filtre sont interroge directement l’entrepôt de données hello
* Les vignettes sont actualisées environ toutes les 15 minutes (actualisation n’est pas nécessaire toobe planifiée)
* Les Questions et réponses ne sont pas disponibles pour les jeux de données de connexion directe.
* Les modifications de schéma ne sont pas récupérées automatiquement.
* Toutes les requêtes de connexion directe expireront après 2 minutes.

Ces restrictions et les notes peuvent changer à mesure que nous tooimprove hello expériences. Hello étapes tooconnect sont détaillées ci-dessous.  

## <a name="using-hello-open-in-power-bi-button"></a>À l’aide du bouton « Ouvrir dans Power BI » de hello
Hello toomove de façon plus simple entre votre entrepôt de données SQL et de Power BI est hello ouvrir du bouton Power BI. Ce bouton vous permet de tooseamlessly commencer à créer de nouveaux tableaux de bord dans Power BI.  

1. tooget démarré accédez l’instance de SQL Data Warehouse tooyour Bonjour portail classique Azure.
2. Cliquez sur le bouton « Ouvrir dans Power BI » de hello.
3. Si nous ne sommes pas en mesure de toosign dans directement, ou si vous n’avez pas un compte Power BI, vous devez toosign dans.  
4. Vous allez être redirigé toohello page de connexion de l’entrepôt de données SQL, avec les informations de hello de votre entrepôt de données SQL est préremplie.
5. Après avoir entré vos informations d’identification, vous serez totalement connecté tooyour SQL Data Warehouse.

## <a name="connecting-through-hello-power-bi-portal"></a>Connexion via le portail de Power BI hello
Bonjour toousing plus ouvrir du bouton Power BI, les utilisateurs peuvent également connecter tootheir SQL Data Warehouse via hello portail Power BI.

1. Cliquez sur « Obtenir les données » en bas de hello hello du volet de navigation.
2. Sélectionnez « Bases de données ».
3. Une fois sur la page de bases de données hello, sélectionnez Azure SQL Data Warehouse, puis sur « Se connecter ».
4. Entrez les informations de connexion nécessaires hello.  Votre nom de serveur et le nom de la base de données sont accessibles dans hello portail Azure.
5. Vous serez dirigé précédent toohello la page principale de Power BI et une fois que votre connexion est établie à une nouvelle entrée sous « Jeux de données » s’affiche avec le nom hello de votre instance.  
6. Vous pouvez cliquer sur hello nouveau dataset tooexplore toutes les tables de hello et des vues dans votre base de données. Sélection d’une colonne enverra une source toohello précédent de requête, créant ainsi dynamiquement votre élément visuel. Ces éléments visuels peuvent être enregistrés dans un nouveau rapport et épinglés dans tooyour le tableau de bord.

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop/
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integration/

<!--MSDN references-->

<!--Other Web references-->
