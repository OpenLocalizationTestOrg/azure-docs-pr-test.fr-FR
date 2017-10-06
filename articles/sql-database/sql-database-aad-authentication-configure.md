---
title: "authentification d’Azure Active Directory aaaConfigure - SQL | Documents Microsoft"
description: "Découvrez comment tooconnect tooSQL base de données et de l’entrepôt de données SQL à l’aide de l’authentification Azure Active Directory."
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
ms.date: 07/10/2017
ms.author: rickbyh
ms.openlocfilehash: d6222da0b840f96d4bcfbc02964dc7c54d5ea1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-manage-azure-active-directory-authentication-with-sql-database-or-sql-data-warehouse"></a>Configurer et gérer l’authentification Azure Active Directory avec SQL Database ou SQL Data Warehouse

Cet article vous montre comment toocreate remplir Azure AD et ensuite utiliser Azure AD avec la base de données SQL Azure et SQL Data Warehouse. Pour obtenir une vue d’ensemble, consultez [Authentification Azure Active Directory](sql-database-aad-authentication.md).

>  [!NOTE]  
>  Connexion tooSQL Server s’exécutant sur une machine virtuelle Azure n’est pas prise en charge d’à l’aide d’un compte Azure Active Directory. Utilisez plutôt un compte Active Directory du domaine.

## <a name="create-and-populate-an-azure-ad"></a>Créer et renseigner un répertoire Azure AD
Créez un annuaire Azure AD et renseignez-le avec les utilisateurs et les groupes. Azure AD peut être le domaine géré de hello initiale de domaine Azure AD. Azure AD peut également être un Services de domaine Active Directory local est fédéré avec hello Azure AD.

Pour plus d’informations, consultez [intégrer vos identités locales avec Azure Active Directory](../active-directory/active-directory-aadconnect.md), [ajouter vos propres tooAzure de nom de domaine Active Directory](../active-directory/active-directory-add-domain.md), [Microsoft Azure prend désormais en charge la fédération avec Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [administrer votre annuaire Azure AD](https://msdn.microsoft.com/library/azure/hh967611.aspx), [gérer Azure Active Directory à l’aide de Windows PowerShell](/powershell/azure/overview?view=azureadps-2.0), et [identité hybride Ports et protocoles requis](../active-directory/active-directory-aadconnect-ports.md).

## <a name="optional-associate-or-change-hello-active-directory-that-is-currently-associated-with-your-azure-subscription"></a>Associer facultatif : Ou modifier hello active directory qui est associé à votre abonnement Azure
tooassociate votre base de données avec le répertoire hello Azure AD pour votre organisation, sélectionnez hello répertoire un approuvé pour la base de données hello hébergement hello abonnement Azure. Pour plus d’informations, consultez la page [Comment sont associés les abonnements Azure et Azure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx).

**Additional information :** chaque abonnement Azure dispose d’une relation d’approbation avec une instance Azure AD. Cela signifie qu’il approuve ce tooauthenticate Active les utilisateurs, les services et les périphériques. Plusieurs abonnements peuvent approuver hello même répertoire, mais un abonnement fait confiance à un seul répertoire. Vous pouvez voir l’annuaire approuvé par votre abonnement sous hello **paramètres** onglet à [https://manage.windowsazure.com/](https://manage.windowsazure.com/). Cette relation de confiance possédant un abonnement à un annuaire diffère de la relation hello ayant un abonnement avec toutes les autres ressources dans Azure (sites Web, bases de données et ainsi de suite), qui sont apparentent à des ressources enfants d’un abonnement. Si un abonnement arrive à expiration, puis accéder à toothose autres ressources associés hello abonnement s’arrête également. Répertoire de hello reste dans Azure, mais vous pouvez associer un autre abonnement à ce répertoire et continuer d’utilisateurs Active Directory toomanage hello. Pour plus d’informations sur les ressources, consultez [Comprendre l’accès aux ressources dans Azure](https://msdn.microsoft.com/library/azure/dn584083.aspx).

Hello procédures suivantes vous montrent comment toochange hello associés active pour un abonnement donné.
1. Se connecter tooyour [portail classique Azure](https://manage.windowsazure.com/) à l’aide d’un administrateur d’abonnement Azure.
2. Dans la bannière de gauche hello, sélectionnez **paramètres**.
3. Vos abonnements s’affichent dans l’écran des paramètres de hello. Hello éventuellement abonnement n’apparaît pas, cliquez sur **abonnements** en haut hello, liste déroulante hello **filtre par répertoire** zone et sélectionnez hello répertoire qui contient vos abonnements, puis cliquez sur **Appliquer**.
   
    ![sélectionner l'abonnement][4]
4. Bonjour **paramètres** zone, cliquez sur votre abonnement, puis cliquez sur **modifier l’annuaire** bas hello de page de hello.
   
    ![portail-paramètres-ad][5]
5. Bonjour **modifier l’annuaire** zone hello Azure Active Directory qui est associé à votre SQL Server ou d’un entrepôt de données SQL et sélectionnez puis cliquez sur la flèche suivant hello.
   
    ![edit-directory-select][6]
6. Bonjour **confirmer** répertoire boîte de dialogue mappage, vérifiez que «**tous les coadministrateurs seront supprimés.**»
   
    ![edit-directory-confirm][7]
7. Cliquez sur le portail de hello cocher tooreload hello.

   > [!NOTE]
   > Lorsque vous modifiez le répertoire de hello, coadministrateurs de tooall accès, Azure AD utilisateurs et groupes et reposant sur le répertoire des ressources utilisateurs sont supprimés et ils n’ont plus accès toothis abonnement ou ses ressources. Uniquement, en tant qu’un administrateur de service, de configurer l’accès pour les principaux basés sur le nouveau répertoire de hello. Cette modification peut prendre beaucoup de ressources de tooall toopropagate de temps. Passage du répertoire de hello, également modifications hello administrateur Azure AD pour la base de données SQL et SQL Data Warehouse et interdire l’accès de base de données pour les utilisateurs Azure AD existants. Hello Azure AD admin doit être réinitialisation (comme décrit ci-dessous) et Azure nouveaux utilisateurs d’Active Directory doivent être créés.
   >  

## <a name="create-an-azure-ad-administrator-for-azure-sql-server"></a>Créer un administrateur d’Azure AD pour le serveur SQL Azure
Chaque serveur SQL Azure (qui héberge la base de données SQL ou SQL Data Warehouse) démarre avec un compte d’administrateur de serveur unique qui est administrateur hello d’ensemble du serveur SQL Azure hello. Un deuxième administrateur SQL Server doit être créé. Il s’agit d’un compte Azure AD. Cette entité de sécurité est créée en tant qu’un utilisateur de base de données contenue dans la base de données master hello. En tant qu’administrateurs, comptes d’administrateur serveur hello sont membres de hello **db_owner** rôle dans tous les utilisateurs de base de données et entrez chaque base de données utilisateur hello **dbo** utilisateur. Pour plus d’informations sur les comptes d’administrateur serveur hello, consultez [gérer les bases de données et des connexions dans base de données SQL Azure](sql-database-manage-logins.md).

Lorsque vous utilisez Azure Active Directory avec la géo-réplication, administrateur de hello Azure Active Directory doit être configuré pour hello principal et les serveurs secondaires hello. Si un serveur n’a pas un administrateur Azure Active Directory, puis les utilisateurs et les connexions d’accès Azure Active Directory une erreur « Impossible de se connecter » tooserver.

> [!NOTE]
> Les utilisateurs qui ne sont pas basées sur un compte Azure AD (y compris le compte d’administrateur hello Azure SQL server), ne peut pas créer Azure AD les utilisateurs, car ils n’ont pas toovalidate autorisation proposé aux utilisateurs de base de données avec Azure AD de hello.
> 

## <a name="provision-an-azure-active-directory-administrator-for-your-azure-sql-server"></a>Approvisionner un administrateur d’Azure Active Directory pour votre serveur Azure SQL

Hello deux procédures suivantes vous montrent comment tooprovision un administrateur Azure Active Directory pour votre serveur SQL Azure Bonjour portail Azure et à l’aide de PowerShell.

### <a name="azure-portal"></a>Portail Azure
1. Bonjour [portail Azure](https://portal.azure.com/)hello coin supérieur droit, cliquez sur dans votre toodrop de connexion vers le bas d’une liste de répertoires Active possibles. Choisissez hello corriger Active Directory comme valeur par défaut de hello Azure AD. Cette étape liens hello abonnement association avec Active Directory avec Azure SQL server assurant que hello même abonnement est utilisée pour Azure AD et SQL Server. (hello Azure SQL server peut héberger de base de données SQL Azure ou d’entrepôt de données SQL Azure.)   
    ![choose-ad][8]   
    
2. Bonjour, sélectionnez de bannière de gauche **serveurs SQL**, sélectionnez votre **SQL server**, puis dans hello **SQL Server** panneau, cliquez sur **l’administrateur Active Directory**.   
3. Bonjour **administrateur Active Directory** panneau, cliquez sur **définition de l’administrateur**.   
    ![sélectionner active directory](./media/sql-database-aad-authentication/select-active-directory.png)  
    
4. Bonjour **ajouter admin** panneau, rechercher un utilisateur, sélectionnez hello ou d’un groupe toobe un administrateur, puis cliquez sur **sélectionnez**. (le panneau d’administration hello Active Directory affiche tous les membres et les groupes de votre annuaire Active Directory. Les utilisateurs ou les groupes grisés ne peuvent être sélectionnés, car ils ne sont pas pris en charge en tant qu’administrateurs Azure AD. (Voir liste hello des administrateurs pris en charge dans hello **Azure AD fonctionnalités et Limitations** section de [utilisez authentification Azure Active Directory pour l’authentification de base de données SQL ou SQL Data Warehouse](sql-database-aad-authentication.md).) Contrôle d’accès basé sur un rôle (RBAC) s’applique uniquement toohello portal et n’est pas propagé tooSQL Server.   
    ![sélectionner l’administrateur](./media/sql-database-aad-authentication/select-admin.png)  
    
5. En haut de hello Hello **administrateur Active Directory** panneau, cliquez sur **enregistrer**.   
    ![enregistrer l’administrateur](./media/sql-database-aad-authentication/save-admin.png)   

processus Hello de la modification d’administrateur de hello peut prendre plusieurs minutes. Nouvel administrateur de hello s’affiche dans hello **administrateur Active Directory** boîte.

   > [!NOTE]
   > Lorsque vous configurez hello Azure AD admin, hello nouveau nom d’administrateur (utilisateur ou groupe) ne peut pas déjà être présente dans la base de données master virtuelle hello en tant qu’un utilisateur de l’authentification SQL Server. Le cas échéant, le programme d’installation de hello Azure AD admin échoue ; annulation de sa création et en indiquant que cet un administrateur (nom) de déjà existent. Dans la mesure où un tel utilisateur de l’authentification de SQL Server n’est pas partie de hello Azure AD, tout effort tooconnect toohello à l’aide de l’authentification Azure AD échoue.
   > 


toolater supprimer un administrateur, en haut de hello Hello **administrateur Active Directory** panneau, cliquez sur **supprimer l’administrateur**, puis cliquez sur **enregistrer**.

### <a name="powershell"></a>PowerShell
toorun applets de commande PowerShell, vous devez toohave Azure PowerShell installé et en cours d’exécution. Pour plus d’informations, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).

tooprovision administrateur Azure AD, exécutez hello suivant de commandes Azure PowerShell :

* Add-AzureRmAccount
* Select-AzureRmSubscription

Applets de commande utilisé tooprovision et gérer Azure AD admin :

| Nom de l’applet de commande | Description |
| --- | --- |
| [Set-AzureRmSqlServerActiveDirectoryAdministrator](/powershell/module/azurerm.sql/set-azurermsqlserveractivedirectoryadministrator) |Approvisionne un administrateur Azure Active Directory pour le serveur Azure SQL Server ou Azure SQL Data Warehouse. (Doit être de l’abonnement actuel de hello.) |
| [Remove-AzureRmSqlServerActiveDirectoryAdministrator](/powershell/module/azurerm.sql/remove-azurermsqlserveractivedirectoryadministrator) |Supprime un administrateur Azure Active Directory pour le serveur Azure SQL Server ou Azure SQL Data Warehouse. |
| [Get-AzureRmSqlServerActiveDirectoryAdministrator](/powershell/module/azurerm.sql/get-azurermsqlserveractivedirectoryadministrator) |Retourne des informations à propos d’un administrateur d’Azure Active Directory actuellement configurée pour le serveur SQL Azure de hello ou Azure SQL Data Warehouse. |

Utilisation de PowerShell de commande get-help toosee plus en détail pour chacune de ces commandes, par exemple ``get-help Set-AzureRmSqlServerActiveDirectoryAdministrator``.

Hello suivant les dispositions de script nommé d’un groupe d’administrateur Azure AD **DBA_Group** (id d’objet `40b79501-b343-44ed-9ce7-da4c8cc7353f`) pour hello **demo_server** serveur dans un groupe de ressources nommé **23-groupe** :

```
Set-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23"
-ServerName "demo_server" -DisplayName "DBA_Group"
```

Hello **DisplayName** paramètre d’entrée accepte le nom d’affichage hello Azure AD ou hello nom d’utilisateur Principal. Par exemple, ``DisplayName="John Smith"`` et ``DisplayName="johns@contoso.com"``. Nom d’affichage est prise en charge pour hello uniquement de groupes Azure AD Azure AD.

> [!NOTE]
> Hello commande Azure PowerShell ```Set-AzureRmSqlServerActiveDirectoryAdministrator``` ne vous empêche pas de l’approvisionnement des administrateurs d’Azure AD pour les utilisateurs non pris en charge. Un utilisateur non pris en charge peut être configuré, mais ne peut pas se connecter à tooa de base de données. 
> 

exemple Hello utilise hello facultatif **ObjectID**:

```
Set-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23"
-ServerName "demo_server" -DisplayName "DBA_Group" -ObjectId "40b79501-b343-44ed-9ce7-da4c8cc7353f"
```

> [!NOTE]
> Bonjour Azure AD **ObjectID** est requis lorsque hello **DisplayName** n’est pas unique. tooretrieve hello **ObjectID** et **DisplayName** valeurs, utilisez la section Active Directory de hello du portail classique Azure et affichez les propriétés de hello d’un utilisateur ou un groupe.
> 

Hello l’exemple suivant retourne des informations sur l’administration hello actuelle Azure AD pour le serveur SQL Azure :

```
Get-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23" -ServerName "demo_server" | Format-List
```

Bonjour à l’exemple suivant supprime un administrateur Azure AD :

```
Remove-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23" -ServerName "demo_server"
```

Vous pouvez également configurer un administrateur d’Active Directory Azure à l’aide des API REST de hello. Pour plus d’informations, consultez [Référence de l’API REST de gestion des services et Opérations sur les bases de données SQL Azure](https://msdn.microsoft.com/library/azure/dn505719.aspx)

### <a name="cli"></a>Interface de ligne de commande  
Vous pouvez également configurer un administrateur Azure AD en appelant hello suivant des commandes CLI :
| Commande | Description |
| --- | --- |
|[az sql server ad-admin create](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#create) |Approvisionne un administrateur Azure Active Directory pour le serveur Azure SQL Server ou Azure SQL Data Warehouse. (Doit être de l’abonnement actuel de hello.) |
|[az sql server ad-admin delete](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#delete) |Supprime un administrateur Azure Active Directory pour le serveur Azure SQL Server ou Azure SQL Data Warehouse. |
|[az sql server ad-admin list](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#list) |Retourne des informations à propos d’un administrateur d’Azure Active Directory actuellement configurée pour le serveur SQL Azure de hello ou Azure SQL Data Warehouse. |
|[az sql server ad-admin update](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#update) |Met à jour administrateur d’Active Directory hello pour un serveur SQL Azure ou d’un entrepôt de données SQL Azure. |

Pour plus d’informations sur les commandes CLI, consultez [SQL Server - az sql server](https://docs.microsoft.com/cli/azure/sql/server).  


## <a name="configure-your-client-computers"></a>Configurer vos ordinateurs clients
Sur tous les ordinateurs clients, à partir de laquelle vos applications ou les utilisateurs se connectent tooAzure base de données SQL ou entrepôt de données SQL Azure à l’aide des identités d’Azure AD, vous devez installer hello suivant logicielle :

* .NET Framework version 4.6 ou ultérieure de [https://msdn.microsoft.com/library/5a4x27ek.aspx](https://msdn.microsoft.com/library/5a4x27ek.aspx).
* Bibliothèque d’authentification Azure Active Directory pour SQL Server (**ADALSQL. DLL**) est disponible dans plusieurs langues (x86 et amd64) à partir du centre de téléchargement hello [Microsoft Active Directory Authentication Library pour Microsoft SQL Server](http://www.microsoft.com/download/details.aspx?id=48742).

Vous pouvez répondre à ces exigences en procédant comme suit :

* L’installation soit [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) ou [SQL Server Data Tools pour Visual Studio 2015](https://msdn.microsoft.com/library/mt204009.aspx) répond aux hello exigence de .NET Framework 4.6.
* SSMS installe la version de hello x86 de **ADALSQL. DLL**.
* SSDT installe la version d’amd64 hello de **ADALSQL. DLL**.
* Hello plus récente de Visual Studio à partir de [téléchargements Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs) répond aux exigences de hello .NET Framework 4.6, mais n’installe pas la version d’amd64 requis hello de **ADALSQL. DLL**.

## <a name="create-contained-database-users-in-your-database-mapped-tooazure-ad-identities"></a>Créer des utilisateurs de base de données dans votre base de données mappée de tooAzure identités AD

L’authentification Active Directory Azure nécessite toobe d’utilisateurs de base de données créé en tant qu’utilisateurs de base de données. Un utilisateur de base de données basé sur une identité Azure AD, est un utilisateur de base de données qui ne dispose pas d’une connexion dans la base de données master hello et quelle identité tooan de mappages dans hello annuaire Azure AD qui est associé à la base de données hello. Bonjour Azure AD identity peut être un compte d’utilisateur ou un groupe. Pour plus d'informations sur les utilisateurs de base de données à relation contenant-contenu, consultez [Utilisateurs de base de données - Rendre votre base de données portable](https://msdn.microsoft.com/library/ff929188.aspx).

> [!NOTE]
> Les utilisateurs de base de données (à l’exception de hello des administrateurs) ne peut pas être créés à l’aide de portail. Rôles RBAC ne sont pas propagé tooSQL serveur, base de données SQL ou SQL Data Warehouse. Les rôles RBAC Azure sont utilisés pour la gestion des ressources Azure et ne s’appliquent pas les autorisations toodatabase. Par exemple, hello **SQL Server collaborateur** rôle n’accorde pas d’accès tooconnect toohello base de données SQL ou SQL Data Warehouse. autorisation d’accès de Hello doit être accordée directement dans la base de données hello à l’aide d’instructions Transact-SQL.
>

toocreate un utilisateur de base de données de contenu basée sur Active Directory Azure (autres que hello administrateur du serveur qui est propriétaire de la base de données hello), se connecter toohello de base de données avec une identité Azure AD, en tant qu’utilisateur au moins hello **ALTER ANY USER** autorisation. Utilisez ensuite hello selon la syntaxe Transact-SQL :

```
CREATE USER <Azure_AD_principal_name> FROM EXTERNAL PROVIDER;
```

*Azure_AD_principal_name* peut être hello nom d’utilisateur principal un nom Azure AD utilisateur ou hello complet pour un groupe d’Azure AD.

**Exemples :** toocreate un utilisateur de base de données qui représente un répertoire Azure AD fédéré ou géré d’utilisateur de domaine :
```
CREATE USER [bob@contoso.com] FROM EXTERNAL PROVIDER;
CREATE USER [alice@fabrikam.onmicrosoft.com] FROM EXTERNAL PROVIDER;
```

toocreate un utilisateur de base de données représentant un répertoire Azure AD ou fédéré de groupe de domaine, fournir de nom d’affichage hello un groupe de sécurité :
```
CREATE USER [ICU Nurses] FROM EXTERNAL PROVIDER;
```

toocreate un utilisateur de base de données qui représente une application qui se connecte à l’aide d’un jeton Azure AD :

```
CREATE USER [appName] FROM EXTERNAL PROVIDER;
```

>  [!TIP]
>  Vous ne peut pas créer directement un utilisateur à partir d’Azure Active Directory que hello Azure Active Directory qui est associé à votre abonnement Azure. Toutefois, les membres d’autres annuaires Active Directory qui sont les utilisateurs importés Bonjour associées à Active Directory (appelés utilisateurs externes) peuvent être ajoutées tooan groupe d’Active Directory dans le locataire hello Active Directory. En créant un utilisateur de base de données pour ce groupe Active Directory, hello utilisateurs à partir de hello externe Active Directory peuvent avoir accès tooSQL de base de données.   

Pour plus d’informations sur la création d’utilisateurs de base de données à relation contenant-contenu basés sur des identités Azure Active Directory, voir [CRÉER UN UTILISATEUR (Transact-SQL)](http://msdn.microsoft.com/library/ms173463.aspx).

> [!NOTE]
> Administrateur d’Azure Active Directory hello suppression pour le serveur SQL Azure empêche tout utilisateur de l’authentification Azure AD de se connecter de toohello server. Si nécessaire, des utilisateurs Azure AD inutilisables peuvent être supprimés manuellement par un administrateur du service Base de données SQL.   

>  [!NOTE]
>  Si vous recevez un **expiration de connexion**, vous devrez peut-être tooset hello `TransparentNetworkIPResolution` paramètre de toofalse de chaîne de connexion hello. Pour plus d’informations, consultez [Problème lié au délai d’expiration de la connexion avec .NET Framework 4.6.1 - TransparentNetworkIPResolution](https://blogs.msdn.microsoft.com/dataaccesstechnologies/2016/05/07/connection-timeout-issue-with-net-framework-4-6-1-transparentnetworkipresolution/).   

   
Lorsque vous créez un utilisateur de base de données, que l’utilisateur reçoit hello **CONNECT** autorisation et peuvent se connecter toothat de base de données en tant que membre de hello **PUBLIC** rôle. Initialement hello uniquement les autorisations utilisateur de toohello disponibles sont les autorisations accordées toohello **PUBLIC** rôle ou des autorisations accordées tooany des groupes Windows qu’ils sont membres de. Une fois que vous devez configurer un utilisateur de base de données Azure contenus basée sur Active Directory, vous pouvez accorder des autorisations supplémentaires de l’utilisateur hello, hello même façon que vous accordez l’autorisation tooany autre type d’utilisateur. En général, accorder des autorisations des rôles de toodatabase et ajoutez les utilisateurs tooroles. Pour plus d’informations, consultez [Notions de base sur les autorisations de moteur de base de données](http://social.technet.microsoft.com/wiki/contents/articles/4433.database-engine-permission-basics.aspx). Pour plus d'informations sur les rôles de base de données SQL, consultez [Gestion des bases de données et des connexions dans la base de données SQL Azure](sql-database-manage-logins.md).
Un domaine fédéré qui sont importées dans un domaine de gestion, vous devez utiliser hello géré l’identité de domaine.

> [!NOTE]
> Les utilisateurs Active Directory Azure sont marquées dans les métadonnées de base de données hello avec type E (EXTERNAL_USER) et pour les groupes avec type X (EXTERNAL_GROUPS). Pour plus d’informations, consultez [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx). 
>

## <a name="connect-toohello-user-database-or-data-warehouse-by-using-ssms-or-ssdt"></a>Se connecter toohello utilisateur de base de données ou du data warehouse à l’aide de SSMS ou SSDT  
tooconfirm hello Azure AD administrateur est correctement configuré, connectez-vous toohello **master** base de données à l’aide du compte d’administrateur hello Azure AD.
tooprovision un utilisateur de base de données de contenu basée sur Active Directory Azure (autres que hello administrateur du serveur qui est propriétaire de la base de données hello), se connecter à base de données toohello avec une identité Azure AD qui a la base de données access toohello.

> [!IMPORTANT]
> La prise en charge de l’authentification Azure Active Directory est disponible avec [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) et [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) dans Visual Studio 2015. Hello version d’août 2016 de SSMS prend également en charge Universal l’authentification Active Directory, qui permet aux administrateurs toorequire multi-Factor Authentication à l’aide d’un appel téléphonique, message texte, les cartes à puce avec code confidentiel ou notification d’application mobile.
 
## <a name="using-an-azure-ad-identity-tooconnect-using-ssms-or-ssdt"></a>À l’aide d’un tooconnect d’identité Azure AD à l’aide de SSMS ou SSDT  

Hello procédures suivantes vous montre comment tooconnect tooa SQL de base de données avec une identité Azure AD à l’aide de SQL Server Management Studio ou les outils de base de données SQL Server.

### <a name="active-directory-integrated-authentication"></a>Authentification intégrée d'Active Directory

Utilisez cette méthode si vous êtes connecté dans tooWindows à l’aide de vos informations d’identification Azure Active Directory à partir d’un domaine fédéré.

1. Démarrez Management Studio ou les outils de données et Bonjour **connecter tooServer** (ou **connecter tooDatabase moteur**) la boîte de dialogue hello **authentification** , sélectionnez **Intégrées à active Directory -**. Aucun mot de passe est nécessaire ou peut être entré, car vos informations d’identification existantes seront présentées pour la connexion de hello.   

    ![Sélectionner l’authentification intégrée AD][11]
2. Cliquez sur hello **Options** bouton, hello et **propriétés de connexion** page hello **connecter toodatabase** zone, entrez un nom hello de base de données utilisateur hello souhaité tooconnect À. (hello **ID de client ou le nom de domaine AD**» option est uniquement prise en charge pour **universel avec la connexion de l’authentification Multifacteur** options, dans le cas contraire elle est grisée.)  

    ![Sélectionnez le nom de base de données hello][13]

## <a name="active-directory-password-authentication"></a>Authentification par mot de passe Active Directory

Utilisez cette méthode lorsque la connexion avec un nom de principal de Azure AD à l’aide d’Azure AD de hello géré de domaine. Vous pouvez également l’utiliser pour un compte fédéré sans domaine toohello d’accès, par exemple, lorsque vous travaillez à distance.

Utilisez cette méthode si vous êtes connecté en tooWindows à l’aide des informations d’identification d’un domaine qui n’est pas fédéré avec Azure, ou lorsque vous utilisez Azure AD à l’aide de l’authentification Azure AD selon hello initiale ou hello domaine client.

1. Démarrez Management Studio ou les outils de données et Bonjour **connecter tooServer** (ou **connecter tooDatabase moteur**) la boîte de dialogue hello **authentification** , sélectionnez **Active Directory - mot de passe**.
2. Bonjour **nom d’utilisateur** , tapez votre nom d’utilisateur Azure Active Directory dans le format de hello  **username@domain.com** . Cela doit être un compte à partir de hello Azure Active Directory ou un compte à partir d’un domaine fédérer avec hello Azure Active Directory.
3. Bonjour **mot de passe** , tapez votre mot de passe utilisateur pour le compte de hello Azure Active Directory ou compte de domaine fédéré.

    ![Sélectionner l’authentification par mot de passe AD][12]
4. Cliquez sur hello **Options** bouton, hello et **propriétés de connexion** page hello **connecter toodatabase** zone, entrez un nom hello de base de données utilisateur hello souhaité tooconnect À. (Consultez le graphique de hello dans l’option précédente de hello.)

## <a name="using-an-azure-ad-identity-tooconnect-from-a-client-application"></a>À l’aide d’un tooconnect d’identité Azure AD à partir d’une application cliente

Hello procédures suivantes vous montre comment tooconnect tooa SQL de base de données avec une identité Azure AD à partir d’une application cliente.

###  <a name="active-directory-integrated-authentication"></a>Authentification intégrée d'Active Directory

toouse l’authentification intégrée Windows, Active Directory de votre domaine doit être fédéré avec Azure Active Directory. Votre application cliente (ou un service de connexion de base de données toohello) doit être en cours d’exécution sur un ordinateur joint au domaine sous les informations d’identification de domaine d’un utilisateur.

à l’aide de base de données tooconnect tooa intégré l’authentification et une identité Azure AD, mot clé d’authentification de hello dans la chaîne de connexion de base de données hello doit avoir la valeur tooActive intégrée active. Hello exemple de code c# suivant utilise ADO .NET.

```
string ConnectionString =
@"Data Source=n9lxnyuzhv.database.windows.net; Authentication=Active Directory Integrated; Initial Catalog=testdb;";
SqlConnection conn = new SqlConnection(ConnectionString);
conn.Open();
```

mot clé de chaîne de connexion de Hello ``Integrated Security=True`` n’est pas prise en charge pour la connexion tooAzure base de données SQL. Lors de l’établissement d’une connexion ODBC, vous devez tooremove espaces et définir l’authentification too'ActiveDirectoryIntegrated'.

### <a name="active-directory-password-authentication"></a>Authentification par mot de passe Active Directory

à l’aide de base de données tooconnect tooa intégré l’authentification et une identité Azure AD, mot clé d’authentification de hello doit avoir la valeur tooActive mot de passe active. chaîne de connexion Hello doit contenir des ID d’utilisateur/UID et mots clés de mot de passe/PWD et de valeurs. Hello exemple de code c# suivant utilise ADO .NET.

```
string ConnectionString =
@"Data Source=n9lxnyuzhv.database.windows.net; Authentication=Active Directory Password; Initial Catalog=testdb;  UID=bob@contoso.onmicrosoft.com; PWD=MyPassWord!";
SqlConnection conn = new SqlConnection(ConnectionString);
conn.Open();
```

En savoir plus sur les méthodes d’authentification Azure AD à l’aide des exemples de code de démonstration hello disponibles à l’adresse [Azure AD d’authentification GitHub démonstration](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/security/azure-active-directory-auth).

## <a name="azure-ad-token"></a>Jeton Azure AD
Cette méthode d’authentification permet de services de couche intermédiaire tooconnect tooAzure base de données SQL ou d’entrepôt de données SQL Azure en obtenant un jeton d’Azure Active Directory (AAD). Elle permet l’utilisation de scénarios complexes, notamment l’authentification par certificat. Vous devez effectuer quatre étapes de base toouse jeton l’authentification Azure AD :

1. Inscrire votre application avec Azure Active Directory et obtenir l’id de client hello pour votre code. 
2. Créez une application hello représentant de base de données utilisateur. (Effectué à l’étape 6.)
3. Créez un certificat sur les exécutions d’ordinateur hello client application hello.
4. Ajouter le certificat de hello en tant que clé pour votre application.

Exemple de chaîne de connexion :

```
string ConnectionString =@"Data Source=n9lxnyuzhv.database.windows.net; Initial Catalog=testdb;"
SqlConnection conn = new SqlConnection(ConnectionString);
connection.AccessToken = "Your JWT token"
conn.Open();
```

Pour plus d’informations, consultez le [Blog de sécurité de SQL Server](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth/).

### <a name="sqlcmd"></a>sqlcmd

Bonjour suivant les instructions, connectez-vous à l’aide de la version 13.1 de sqlcmd, qui est disponible à partir de hello [centre de téléchargement](http://go.microsoft.com/fwlink/?LinkID=825643).

```
sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net  -G  
sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net -U bob@contoso.com -P MyAADPassword -G -l 30
```

## <a name="next-steps"></a>Étapes suivantes
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
[10]: ./media/sql-database-aad-authentication/10choose-admin.png
[11]: ./media/sql-database-aad-authentication/active-directory-integrated.png
[12]: ./media/sql-database-aad-authentication/12connect-using-pw-auth2.png
[13]: ./media/sql-database-aad-authentication/13connect-to-db2.png

