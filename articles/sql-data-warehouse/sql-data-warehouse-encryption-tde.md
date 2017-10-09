---
title: "aaaTransparent chiffrement des données dans l’entrepôt de données SQL (portail) | Documents Microsoft"
description: "Chiffrement transparent des données (TDE) dans SQL Data Warehouse"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: fabf75d3-9bbf-4e0d-9b31-8b5a8713f08d
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 8233886ecf170844104e0d1459e2a829cafa9b8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-transparent-data-encryption-tde-in-sql-data-warehouse"></a>Mise en route avec le chiffrement transparent des données (TDE) dans SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Présentation de la sécurité](sql-data-warehouse-overview-manage-security.md)
> * [Authentification](sql-data-warehouse-authentication.md)
> * [Chiffrement (portail)](sql-data-warehouse-encryption-tde.md)
> * [Chiffrement (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a>Autorisations requises
tooenable Transparent Data Encryption (TDE), vous devez être un administrateur ou un membre du rôle dbmanager de hello.

## <a name="enabling-encryption"></a>Activation du chiffrement
tooenable chiffrement transparent des données d’un entrepôt de données SQL, suivez les étapes de hello ci-dessous :

1. Base de données ouverte hello Bonjour [portail Azure](https://portal.azure.com)
2. Dans le panneau de la base de données hello, cliquez sur hello **paramètres** bouton
3. Sélectionnez hello **chiffrement Transparent des données** option![][1]
4. Sélectionnez hello **sur** paramètre![][2]
5. Sélectionnez **Enregistrer**
   ![][3]  

## <a name="disabling-encryption"></a>Désactivation du chiffrement
toodisable chiffrement transparent des données d’un entrepôt de données SQL, suivez les étapes de hello ci-dessous :

1. Base de données ouverte hello Bonjour [portail Azure](https://portal.azure.com)
2. Dans le panneau de la base de données hello, cliquez sur hello **paramètres** bouton
3. Sélectionnez hello **chiffrement Transparent des données** option![][1]
4. Sélectionnez hello **hors** paramètre![][4]
5. Sélectionnez **Enregistrer**
   ![][5]  

## <a name="encryption-dmvs"></a>DMV de chiffrement
Le chiffrement peut être confirmé par hello suivant des vues de gestion dynamique :

* [sys.databases]
* [sys.dm_pdw_nodes_database_encryption_keys]

<!--MSDN references-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings.png
[2]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-on.png
[3]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save.png
[4]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-off.png
[5]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save2.png

<!--Link references-->
