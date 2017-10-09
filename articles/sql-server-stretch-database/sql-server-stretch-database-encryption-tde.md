---
title: "aaaEnable chiffrement Transparent des données pour Stretch Database - Azure | Documents Microsoft"
description: "Activer le chiffrement transparent des données (TDE) pour SQL Server Stretch Database sur Azure"
services: sql-server-stretch-database
documentationcenter: 
author: douglaslMS
manager: barbkess
editor: 
ms.assetid: a44ed8f5-b416-4c41-9b1e-b7271f10bdc3
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2016
ms.author: douglasl
ms.openlocfilehash: 1d6bff455030ac8851b2184c1e8097afd61361d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure"></a>Activer le chiffrement transparent des données (TDE) pour Stretch Database sur Azure
> [!div class="op_single_selector"]
> * [Portail Azure](sql-server-stretch-database-encryption-tde.md)
> * [TSQL](sql-server-stretch-database-tde-tsql.md)
>
>

Chiffrement transparent des données (TDE) vous aide à protéger contre les menaces hello d’activités malveillantes en effectuant le chiffrement en temps réel et le déchiffrement de la base de données de hello, les sauvegardes associées et les fichiers journaux des transactions au repos sans nécessiter de modifications toohello application.

Stockage hello d’une base de données entière est chiffré à l’aide d’une clé de chiffrement de base de données hello appelée de clé symétrique. clé de chiffrement de base de données Hello est protégé par un certificat de serveur intégré. certificat de serveur intégré Hello est unique pour chaque serveur Azure. Microsoft alterne automatiquement ces certificats au moins tous les 90 jours. Pour obtenir une description générale du chiffrement transparent des données, consultez [Chiffrement transparent des données (TDE)].

## <a name="enabling-encryption"></a>Activation du chiffrement
tooenable chiffrement transparent des données pour une base de données Azure stocke hello les données migrées à partir d’une base de données SQL Server compatible Stretch, hello suivant choses :

1. Base de données ouverte hello Bonjour [portail Azure](https://portal.azure.com)
2. Dans le panneau de la base de données hello, cliquez sur hello **paramètres** bouton
3. Sélectionnez hello **chiffrement Transparent des données** option![][1]
4. Sélectionnez hello **sur** définition, puis sélectionnez **enregistrer**
   ![][2]

## <a name="disabling-encryption"></a>Désactivation du chiffrement
toodisable chiffrement transparent des données pour une base de données Azure stocke hello les données migrées à partir d’une base de données SQL Server compatible Stretch, hello suivant choses :

1. Base de données ouverte hello Bonjour [portail Azure](https://portal.azure.com)
2. Dans le panneau de la base de données hello, cliquez sur hello **paramètres** bouton
3. Sélectionnez hello **chiffrement Transparent des données** option
4. Sélectionnez hello **hors** définition, puis sélectionnez **enregistrer**

<!--Anchors-->
[Chiffrement transparent des données (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->
[1]: ./media/sql-server-stretch-database-encryption-tde/stretchtde1.png
[2]: ./media/sql-server-stretch-database-encryption-tde/stretchtde2.png


<!--Link references-->
