---
title: "authentification Active Directory d’aaaAzure - SQL de Azure (aperçu) | Documents Microsoft"
description: "En savoir plus sur la façon de toouse Azure Active Directory pour l’authentification de base de données SQL et SQL Data Warehouse"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 7e2508a1-347e-4f15-b060-d46602c5ce7e
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 08/11/2017
ms.author: rickbyh
ms.openlocfilehash: 7a63a162653b65294e11d3fa5bf39c320e742854
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-active-directory-authentication-for-authentication-with-sql-database-or-sql-data-warehouse"></a>Utiliser l’authentification Azure Active Directory pour l’authentification auprès de SQL Database ou de SQL Data Warehouse
L’authentification Azure Active Directory est un mécanisme de connexion de base de données SQL Azure de tooMicrosoft et [SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) à l’aide des identités dans Azure Active Directory (Azure AD). Avec l’authentification Azure AD, vous pouvez gérer de manière centralisée les identités hello d’utilisateurs de base de données et d’autres services de Microsoft dans un emplacement central. Gestion des ID fournit un emplacement unique aux utilisateurs de base de données de toomanage et simplifie la gestion de l’autorisation. Avantages hello suivants :

* Il fournit une authentification de serveur alternatif tooSQL.
* Vous aide à arrêter la prolifération hello des identités des utilisateurs sur les serveurs de base de données.
* Permet la rotation de mot de passe à un emplacement unique
* Les clients peuvent gérer les autorisations de base de données à l’aide de groupes (AAD) externes.
* Il peut éliminer le stockage des mots de passe en activant l’authentification intégrée Windows et les autres formes d’authentification prises en charge par Azure Active Directory.
* L’authentification Azure AD utilise la relation contenant-contenu de la base de données utilisateurs tooauthenticate identités au niveau de base de données hello.
* Azure AD prend en charge l’authentification basée sur le jeton pour les applications qui se connectent tooSQL de base de données.
* L’authentification Azure AD prend en charge ADFS (fédération de domaine) ou l’authentification utilisateur natif/mot de passe pour un répertoire Azure Active Directory local sans synchronisation du domaine.  
* Azure AD prend en charge les connexions à partir de SQL Server Management Studio qui utilisent l’authentification universelle Active Directory, et notamment Multi-Factor Authentication (MFA).  MFA comprend une authentification forte avec une gamme d’options de vérification simples (appel téléphonique, SMS, cartes à puce avec code PIN ou notification d’application mobile). Pour plus d’informations, voir [Prise en charge de SSMS pour Azure AD MFA avec la base de données SQL et SQL Data Warehouse](sql-database-ssms-mfa-authentication.md).  

>  [!NOTE]  
>  Connexion tooSQL Server s’exécutant sur une machine virtuelle Azure n’est pas prise en charge d’à l’aide d’un compte Azure Active Directory. Utilisez plutôt un compte Active Directory du domaine.  

étapes de configuration Hello incluent hello suivant les procédures tooconfigure et utilisent l’authentification Azure Active Directory.

1. Créer et renseigner Azure AD.
2. Associer facultatif : Ou modifier hello active directory qui est associé à votre abonnement Azure.
3. Créer un administrateur Azure Active Directory pour le serveur Azure SQL Server ou pour [Azure SQL Data Warehouse](https://azure.microsoft.com/services/sql-data-warehouse/).
4. Configurer vos ordinateurs clients.
5. Créer des utilisateurs de base de données dans votre base de données mappée de tooAzure identités AD.
6. Se connecter tooyour de base de données à l’aide d’identités Azure AD.

> [!NOTE]
> toolearn comment toocreate et remplir Azure AD et ensuite configurer Azure AD avec la base de données SQL Azure et SQL Data Warehouse, consultez [configurer Azure AD avec Azure SQL Database](sql-database-aad-authentication-configure.md).
>

## <a name="trust-architecture"></a>Architecture d’approbation
Hello suivant le diagramme résume l’architecture de la solution de l’utilisation de l’authentification Azure Active Directory avec la base de données SQL Azure hello. Hello concepts s’appliquent tooSQL l’entrepôt de données. toosupport Azure AD natif mot de passe utilisateur, uniquement la partie de Cloud de hello et la base de données SQL Azure AD/Azure est pris en compte. toosupport l’authentification fédérée (ou un utilisateur/mot de passe pour les informations d’identification Windows), la communication avec ADFS bloc hello est nécessaire. flèches de Hello indiquent des voies de communication.

![diagramme autorisation aad][1]

Hello diagramme suivant indique hello federation, approbation et les relations qui permettent à un client de base de données de tooconnect tooa en envoyant un jeton d’hébergement. jeton de Hello est authentifié par Azure Active Directory et est approuvé par la base de données hello. Le client 1 peut représenter un répertoire Azure Active Directory avec des utilisateurs natifs ou un répertoire Azure AD avec des utilisateurs fédérés. Le client 2 représente une solution possible incluant des utilisateurs importés, qui dans cet exemple proviennent d’un répertoire Azure Active Directory fédéré avec la synchronisation d’ADFS avec Azure Active Directory. Il est important de toounderstand qui accèdent à la base de données tooa à l’aide de l’authentification Azure AD nécessite que hello hébergeant l’abonnement est associé toohello Azure AD. même abonnement Hello doit être utilisé toocreate hello SQL hébergement messages hello du serveur base de données SQL Azure ou SQL Data Warehouse.

![relation abonnement][2]

## <a name="administrator-structure"></a>Structure de l’administrateur
Lorsque vous utilisez l’authentification Azure AD, il existe deux comptes d’administrateur pour le serveur de base de données SQL hello ; Bonjour administrateur SQL Server d’origine et l’administrateur de hello Azure AD. Hello concepts s’appliquent tooSQL l’entrepôt de données. Seul l’administrateur hello basé sur un compte Azure AD peut créer le premier utilisateur de base de données Azure AD contenu hello dans une base de données utilisateur. connexion de l’administrateur Azure AD Hello peut être un utilisateur Azure AD ou un groupe AD Azure. Lorsque l’administrateur de hello est un compte de groupe, il peut être utilisé par n’importe quel membre du groupe, l’activation de plusieurs administrateurs Azure AD pour l’instance de SQL Server hello. À l’aide du compte de groupe comme un administrateur améliore la facilité de gestion en vous toocentrally ajouter et supprimer des membres du groupe dans Azure AD sans modifier les utilisateurs de hello ou des autorisations de base de données SQL. Seul un administrateur Azure AD (utilisateur ou groupe) peut être configuré à tout moment.

![structure admin][3]

## <a name="permissions"></a>Autorisations
toocreate de nouveaux utilisateurs, vous devez disposer hello `ALTER ANY USER` autorisation dans la base de données hello. Hello `ALTER ANY USER` autorisation peut être accordée à utilisateur de base de données tooany. Hello `ALTER ANY USER` autorisation est également détenue par les comptes d’administrateur serveur hello et les utilisateurs de base de données avec hello `CONTROL ON DATABASE` ou `ALTER ON DATABASE` autorisation pour cette base de données et par les membres de hello `db_owner` rôle de base de données.

toocreate un utilisateur de base de données contenue dans la base de données SQL Azure ou SQL Data Warehouse, vous devez vous connecter à l’aide d’une identité Azure AD de la base de données toohello. toocreate hello première relation contenant-contenu utilisateur base de données, vous devez vous connecter à des toohello de base de données à l’aide d’un administrateur Azure AD (qui est propriétaire de hello de base de données hello). Cette opération est illustrée dans les étapes 4 et 5 ci-dessous. Aucune authentification Azure AD est uniquement possible si hello Azure AD admin a été créé pour le serveur de base de données SQL Azure ou SQL Data Warehouse. Si l’administrateur d’Azure Active Directory hello a été supprimé hello serveur, les utilisateurs Azure Active Directory existants créés précédemment à l’intérieur de SQL Server peuvent ne plus se connecter toohello de base de données à l’aide de leurs informations d’identification Azure Active Directory.

## <a name="azure-ad-features-and-limitations"></a>Limitations et fonctionnalités azure AD
Hello suivant des membres d’Azure AD peut être configurée dans Azure SQL server ou SQL Data Warehouse :

* Membres natives : un membre créé dans Azure AD dans le domaine géré de hello ou dans un domaine de client. Pour plus d’informations, consultez [ajouter vos propres tooAzure de nom de domaine Active Directory](../active-directory/active-directory-add-domain.md).
* Membre de domaine fédéré : un membre créé dans Azure AD avec un domaine fédéré. Pour plus d’informations, consultez [Microsoft Azure prend désormais en charge la fédération avec Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/).
* Membres importés à partir d’autres répertoires Azure AD qui sont des membres natifs ou de domaine fédéré.
* Groupes Active Directory créés en tant que groupes de sécurité.

Les comptes Microsoft (par exemple outlook.com, hotmail.com, live.com) ou d’autres comptes d’invité (par exemple gmail.com, yahoo.com) ne sont pas pris en charge. Si vous pouvez vous connecter trop[https://login.live.com](https://login.live.com) hello et mot de passe, puis vous utilisez un compte Microsoft, qui ne sont pas pris en charge pour l’authentification d’Azure AD pour la base de données SQL Azure ou Azure SQL Data Warehouse.

## <a name="connecting-using-azure-ad-identities"></a>Connexion à l’aide des identités Azure AD

L’authentification Azure Active Directory prend en charge hello suivant les méthodes de connexion de base de données tooa à l’aide d’identités Azure AD :

* À l’aide de l’authentification Windows.
* À l’aide d’un nom principal et d’un mot de passe Azure AD
* À l’aide de l’authentification par jeton d’application

### <a name="additional-considerations"></a>Considérations supplémentaires

* tooenhance facilité de gestion, il est recommandé de vous fournir une publicité Azure dédiée groupe en tant qu’administrateur.   
* Un seul utilisateur administrateur Azure AD (utilisateur ou groupe) peut être configuré pour un serveur Azure SQL Server ou Azure SQL Data Warehouse à tout moment.   
* Seul un administrateur Azure AD pour SQL Server peut se connecter initialement serveur SQL Azure de toohello ou Azure SQL Data Warehouse à l’aide d’un compte Azure Active Directory. administrateur d’Active Directory Hello peut configurer AD Azure suivante aux utilisateurs de base de données.   
* Nous vous recommandons de définir hello connexion délai too30 (secondes).   
* SQL Server 2016 Management Studio et SQL Server Data Tools pour Visual Studio 2015 (version 14.0.60311.1 d’avril 2016 ou ultérieure) prennent en charge l’authentification Azure Active Directory. (L’authentification azure AD est pris en charge par hello **fournisseur de données .NET Framework pour SQL Server**; au moins la version .NET Framework 4.6). Par conséquent hello dernières versions de ces outils et applications de couche données (DAC et .bacpac) peuvent utiliser l’authentification Azure AD.   
* [ODBC version 13.1`bcp.exe` prend en charge l’authentification Azure Active Directory. Toutefois ](https://www.microsoft.com/download/details.aspx?id=53339) ne peut pas se connecter avec l’authentification Azure Active Directory car il utilise un fournisseur ODBC plus ancien.   
* `sqlcmd`prend en charge le début de l’authentification Azure Active Directory avec la version 13.1 disponibles à partir de hello [centre de téléchargement](http://go.microsoft.com/fwlink/?LinkID=825643).   
* SQL Server Data Tools pour Visual Studio 2015 requiert au moins version d’avril 2016 hello Hello Data Tools (version 14.0.60311.1). Actuellement, les utilisateurs Azure AD ne sont pas affichés dans l’Explorateur d’objets SSDT. Pour résoudre ce problème, afficher les utilisateurs de hello dans [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).   
* Le [pilote Microsoft JDBC 6.0 pour SQL Server](https://www.microsoft.com/download/details.aspx?id=11774) prend en charge l’authentification Azure AD. Consultez également [définition des propriétés de connexion hello](https://msdn.microsoft.com/library/ms378988.aspx).   
* PolyBase ne peut pas s’authentifier avec l’authentification Azure AD.   
* L’authentification Azure AD est pris en charge pour la base de données SQL par hello portail Azure **base de données d’importation** et **exporter la base de données** lames. Importation et exportation à l’aide de l’authentification Azure AD est également pris en charge à partir de la commande PowerShell de hello.   
* L’authentification Azure AD est prise en charge pour SQL Database et SQL Data Warehouse via l’interface de ligne de commande (CLI). Pour plus d’informations, consultez [Configurer et gérer l’authentification Azure Active Directory avec SQL Database ou SQL Data Warehouse](sql-database-aad-authentication-configure.md) et [SQL Server - az sql server](https://docs.microsoft.com/en-us/cli/azure/sql/server).

## <a name="next-steps"></a>Étapes suivantes
- toolearn comment toocreate et remplir Azure AD et ensuite configurer Azure AD avec la base de données SQL Azure ou Azure SQL Data Warehouse, consultez [configurer et gérer l’authentification d’Azure Active Directory avec la base de données SQL ou SQL Data Warehouse](sql-database-aad-authentication-configure.md).
- Pour obtenir une vue d’ensemble de l’accès et du contrôle dans la base de données SQL, voir [Accès à la base de données SQL et contrôle](sql-database-control-access.md).
- Pour une vue d’ensemble des connexions, des utilisateurs et des rôles de base de données dans la base de données SQL, voir [Connexions, utilisateurs et rôles de base de données](sql-database-manage-logins.md).
- Pour en savoir plus sur les principaux de base de données, voir [Principaux](https://msdn.microsoft.com/library/ms181127.aspx).
- Pour en savoir plus sur les rôles de base de données, voir [Rôles de base de données](https://msdn.microsoft.com/library/ms189121.aspx).
- Pour en savoir plus sur les règles de pare-feu dans la base de données SQL, voir [Règles de pare-feu de la base de données SQL](sql-database-firewall-configure.md).

<!--Image references-->

[1]: ./media/sql-database-aad-authentication/1aad-auth-diagram.png
[2]: ./media/sql-database-aad-authentication/2subscription-relationship.png
[3]: ./media/sql-database-aad-authentication/3admin-structure.png
[4]: ./media/sql-database-aad-authentication/4select-subscription.png
[5]: ./media/sql-database-aad-authentication/5ad-settings-portal.png
[6]: ./media/sql-database-aad-authentication/6edit-directory-select.png
[7]: ./media/sql-database-aad-authentication/7edit-directory-confirm.png
[8]: ./media/sql-database-aad-authentication/8choose-ad.png
[9]: ./media/sql-database-aad-authentication/9ad-settings.png
[10]: ./media/sql-database-aad-authentication/10choose-admin.png
[11]: ./media/sql-database-aad-authentication/11connect-using-int-auth.png
[12]: ./media/sql-database-aad-authentication/12connect-using-pw-auth.png
[13]: ./media/sql-database-aad-authentication/13connect-to-db.png

