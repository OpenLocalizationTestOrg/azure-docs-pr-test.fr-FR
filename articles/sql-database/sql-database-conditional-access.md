---
title: "aaaConditional accès - base de données SQL Azure et l’entrepôt de données | Documentation de Microsoft"
description: "Découvrez comment tooconfigure d’accès conditionnel pour la base de données SQL Azure et l’entrepôt de données."
services: sql-database
author: BYHAM
manager: jhubbard
ms.custom: security
ms.service: sql-database
ms.topic: article
ms.date: 06/07/2017
ms.author: rickbyh
ms.openlocfilehash: f49f4708c0f1b3cad1539d630c2efd919f8ece68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-mfa-with-azure-sql-database-and-data-warehouse"></a>Accès conditionnel (MFA) avec Azure SQL Database et Data Warehouse  

SQL Database et SQL Data Warehouse prennent tous deux en charge l’accès conditionnel Microsoft. Hello suivant les étapes indiquent comment tooenforce de base de données SQL tooconfigure une stratégie d’accès conditionnel.  

## <a name="prerequisites"></a>Composants requis  
- Vous devez configurer l’authentification d’Azure Active Directory toosupport base de données SQL ou SQL Data Warehouse. Pour connaître la procédure spécifique, consultez [Configurer et gérer l’authentification Azure Active Directory avec SQL Database ou SQL Data Warehouse](sql-database-aad-authentication-configure.md).  
- Lorsque l’authentification multifacteur est activée, vous devez vous connecter avec à un outil pris en charge, telles que la dernière version de SSMS de hello. Pour plus d’informations, consultez [Configurer Azure SQL Database Multi-Factor Authentication pour SQL Server Management Studio](sql-database-ssms-mfa-authentication-configure.md).  

## <a name="configure-ca-for-azure-sql-dbdw"></a>Configurer l’accès conditionnel pour Azure SQL DB/DW  
1.  Connexion toohello portail, sélectionnez **Azure Active Directory**, puis sélectionnez **accès conditionnel**. Pour plus d’informations, consultez [Référence technique de l’accès conditionnel Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-conditional-access-technical-reference).  
  ![panneau d’accès conditionnel](./media/sql-database-conditional-access/conditional-access-blade.png) 
     
2.  Bonjour **stratégies d’accès conditionnel** panneau, cliquez sur **nouvelle stratégie**, fournissez un nom, puis cliquez sur **configurer des règles**.  
3.  Sous **affectations**, sélectionnez **utilisateurs et groupes**, vérifiez **sélectionnez utilisateurs et groupes**, puis sélectionnez l’utilisateur de hello ou un groupe pour l’accès conditionnel. Cliquez sur **sélectionnez**, puis cliquez sur **fait** tooaccept votre sélection.  
  ![sélectionner des utilisateurs et des groupes](./media/sql-database-conditional-access/select-users-and-groups.png)  

4.  Sélectionnez **Applications cloud**, puis cliquez sur **Sélectionner des applications**. Vous voyez toutes les applications disponibles pour l’accès conditionnel. Sélectionnez **base de données SQL Azure**, au bas de hello cliquez sur **sélectionnez**, puis cliquez sur **fait**.  
  ![sélectionner SQL Database](./media/sql-database-conditional-access/select-sql-database.png)  
  Si vous ne trouvez pas **base de données SQL Azure** répertorié dans hello suivant capture d’écran tiers, terminer hello comme suit :   
  - Connectez-vous à l’instance d’Azure SQL DB/DW tooyour à l’aide de SSMS avec un compte d’administrateur AAD.  
  - Exécutez `CREATE USER [user@yourtenant.com] FROM EXTERNAL PROVIDER`.  
  - Connectez-vous à tooAAD et vérifiez que la base de données SQL Azure et l’entrepôt de données sont répertoriés dans les applications hello dans votre annuaire AAD.  

5.  Sélectionnez **accéder aux contrôles**, sélectionnez **Grant**, puis vérifiez la stratégie hello tooapply. Pour cet exemple, nous sélectionnons **Imposer l’authentification multifacteur**.  
  ![sélectionner Accorder l’accès](./media/sql-database-conditional-access/grant-access.png)  

## <a name="summary"></a>Résumé  
application de Hello sélectionné (de base de données SQL Azure) qui permet de tooconnect tooAzure SQL DB/DW à l’aide d’Azure AD Premium, applique désormais une stratégie d’accès conditionnel hello sélectionné, **d’authentification multifacteur requis.**  
Pour toute question sur Azure SQL Database et Data Warehouse en ce qui concerne Multi-Factor Authentication, contactez MFAforSQLDB@microsoft.com.  

## <a name="next-steps"></a>Étapes suivantes  

Pour obtenir un didacticiel, consultez [Sécuriser votre base de données Azure SQL Database](sql-database-security-tutorial.md).
