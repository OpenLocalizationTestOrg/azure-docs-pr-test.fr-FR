---
title: "l’authentification multifacteur aaaConfigure - SQL Azure | Documents Microsoft"
description: "Utilisez l’authentification multi-facteur avec SSMS pour la base de données SQL et SQL Data Warehouse."
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/17/2017
ms.author: rickbyh
ms.openlocfilehash: acb275965f4199f7d5e1378d5077824a9bbc80e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multi-factor-authentication-for-sql-server-management-studio-and-azure-ad"></a>Configurer l’authentification multifacteur pour SQL Server Management Studio et Azure AD

Cette rubrique vous montre comment toouse Azure Active Directory l’authentification multifacteur (MFA) avec SQL Server Management Studio. Azure AD MFA peut servir lors de la connexion de SSMS ou SqlPackage.exe tooAzure base de données SQL et Azure SQL Data Warehouse.

Pour une vue d’ensemble de l’authentification multifacteur Azure SQL Database, consultez [Authentification universelle avec SQL Database et SQL Data Warehouse (prise en charge de SSMS pour MFA)](sql-database-ssms-mfa-authentication.md).

## <a name="configuration-steps"></a>Configuration

1. **Configurer Azure Active Directory** - pour plus d’informations, consultez [administrer votre annuaire Azure AD](https://msdn.microsoft.com/library/azure/hh967611.aspx), [intégrer vos identités locales avec Azure Active Directory](../active-directory/active-directory-aadconnect.md), [Ajouter vos propres tooAzure de nom de domaine Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [Microsoft Azure prend désormais en charge la fédération avec Active Directory Windows Server](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), et [gérer Azure Active Directory à l’aide de Windows PowerShell ](https://msdn.microsoft.com/library/azure/jj151815.aspx).
2. **Configurer l’authentification MFA** : pour obtenir des instructions pas à pas, consultez [Présentation d’Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) et [Accès conditionnel (MFA) avec Azure SQL Database et Data Warehouse](sql-database-conditional-access.md). (L’accès conditionnel complet requiert un annuaire Azure Active Directory (Azure AD) Premium. L’authentification MFA limitée est disponible avec un annuaire Azure AD standard.)
3. **Configurer la base de données SQL ou de l’entrepôt de données SQL pour l’authentification Azure AD** - pour obtenir des instructions, consultez [tooSQL de connexion de base de données ou SQL données entrepôt par à l’aide d’authentification Azure Active Directory](sql-database-aad-authentication.md).
4. **Télécharger SSMS** - sur l’ordinateur client de hello, télécharger hello la dernière version de SSMS, à partir de [télécharger SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx). Pour toutes les fonctionnalités de hello dans cette rubrique, utilisez au moins 2017 juillet, version 17,2.  

## <a name="connecting-by-using-universal-authentication-with-ssms"></a>Connexion à l’aide de l’authentification universelle avec SSMS

Hello suit montrent comment tooconnect tooSQL base de données ou l’entrepôt de données SQL à l’aide de hello la dernière version de SSMS.

1. tooconnect à l’aide de l’authentification universelle, sur hello **connecter tooServer** boîte de dialogue, sélectionnez **Active Directory - universel avec prise en charge l’authentification Multifacteur**. (Si vous voyez **l’authentification Active Directory universel** vous n’êtes pas sur la version la plus récente de SSMS hello.)  
   ![1mfa-universal-connect][1]  
2. Hello complète **nom d’utilisateur** zone avec des informations d’identification du Azure Active Directory hello, dans le format de hello `user_name@domain.com`.  
   ![1mfa-universal-connect-user](./media/sql-database-ssms-mfa-auth/1mfa-universal-connect-user.png)   
3. Si vous vous connectez en tant qu’invité, vous devez cliquer sur **Options**et sur hello **propriété de connexion** boîte de dialogue, hello complète **ID de client ou le nom de domaine Active Directory** boîte. Pour plus d’informations, consultez [Authentification universelle avec SQL Database et SQL Data Warehouse (prise en charge de SSMS pour MFA)](sql-database-ssms-mfa-authentication.md).
   ![mfa-tenant-ssms](./media/sql-database-ssms-mfa-auth/mfa-tenant-ssms.png)   
4. Comme d’habitude pour la base de données SQL et SQL Data Warehouse, vous devez cliquer sur **Options** et spécifier la base de données hello sur hello **Options** boîte de dialogue. (Si hello connecté utilisateur est un utilisateur invité (c'est-à-dire joe@outlook.com), vous devez hello case à cocher et ajouter l’ID de client ou le nom du domaine hello AD actuelle dans le cadre des Options. Consultez [Authentification universelle avec SQL Database et SQL Data Warehouse (prise en charge de SSMS pour MFA)]()(sql-database-ssms-mfa-authentication.md). Puis, cliquez sur **Se connecter**.  
5. Hello lorsque **tooyour compte de connexion** boîte de dialogue s’affiche, fournissez hello et mot de passe de votre identité Azure Active Directory. Aucun mot de passe n’est requis si un utilisateur fait partie d’un domaine fédéré avec Azure AD.  
   ![2mfa-sign-in][2]  

   > [!NOTE]
   > Pour l’authentification universelle avec un compte qui ne nécessite pas MFA, vous vous connectez à ce stade. Pour les utilisateurs d’exiger l’authentification Multifacteur, poursuivre hello comme suit :
   >  
   
6. Deux boîtes de dialogue de configuration de MFA peuvent s’afficher. Une seule fois opération varie selon l’administrateur de l’authentification Multifacteur hello définition et peut donc facultatif. Pour un domaine d’authentification Multifacteur activée, cette étape n’est parfois prédéfinie (par exemple, domaine de hello nécessite les utilisateurs toouse une carte à puce et un code confidentiel).  
   ![3mfa-setup][3]  
7. Bonjour deuxième possible une fois la boîte de dialogue vous permet de détails de hello tooselect de votre méthode d’authentification. les options possibles Hello sont configurées par votre administrateur.  
   ![4mfa-verify-1][4]  
8. Bonjour Azure Active Directory envoie hello tooyou des informations de confirmation. Lorsque vous recevez le code de vérification hello, entrez-le dans hello **entrer le code de vérification** , puis cliquez sur **connectez-vous**.  
   ![5mfa-verify-2][5]  

Lorsque la vérification est terminée, SSMS se connecte normalement à condition que les informations d’identification soient valides et qu’un accès au pare-feu soit possible.

## <a name="next-steps"></a>Étapes suivantes

* Pour une vue d’ensemble de l’authentification multifacteur Azure SQL Database, consultez [Authentification universelle avec SQL Database et SQL Data Warehouse (prise en charge de SSMS pour MFA)](sql-database-ssms-mfa-authentication.md).
* Accorder à d’autres d’accès de la base de données tooyour : [l’authentification de base de données SQL et d’autorisation : octroi de l’accès](sql-database-manage-logins.md)  
Assurez-vous que d’autres personnes peuvent se connecter via le pare-feu hello : [règle de pare-feu de configurer un base de données SQL Azure au niveau du serveur à l’aide de hello le portail Azure](sql-database-configure-firewall-settings.md)


[1]: ./media/sql-database-ssms-mfa-auth/1mfa-universal-connect.png
[2]: ./media/sql-database-ssms-mfa-auth/2mfa-sign-in.png
[3]: ./media/sql-database-ssms-mfa-auth/3mfa-setup.png
[4]: ./media/sql-database-ssms-mfa-auth/4mfa-verify-1.png
[5]: ./media/sql-database-ssms-mfa-auth/5mfa-verify-2.png

