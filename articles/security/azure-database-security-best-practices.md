---
title: "meilleures pratiques de la sécurité de base de données aaaAzure | Documents Microsoft"
description: "Cet article fournit un ensemble de meilleures pratiques pour la sécurité des bases de données Azure."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2017
ms.author: tomsh
ms.openlocfilehash: 78984291e8f74879c7f738e2ce3176c4be18d154
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-security-best-practices"></a>Meilleures pratiques en matière de sécurité pour les bases de données Azure

La sécurité est une préoccupation majeure lors de la gestion de bases de données, et elle a toujours été une priorité pour Azure SQL Database. Vos bases de données peuvent être parfaitement sécurisé toohelp satisfaire plus réglementaires ou des exigences de sécurité, notamment HIPAA et PCI DSS niveau 1, ISO 27001/27002. Liste actuelle des certifications de conformité de sécurité est disponible à l’adresse hello [site de Microsoft Trust Center](http://azure.microsoft.com/support/trust-center/services/). Vous pouvez également choisir tooplace vos bases de données dans des centres de données Azure spécifique basées sur le respect des obligations réglementaires.

Dans cet article, nous aborderons différentes meilleures pratiques en matière de sécurité pour les bases de données Azure. Ces recommandations sont dérivées de notre expérience avec la sécurité de la base de données Azure et les expériences hello de clients comme vous-même.

Pour chaque bonne pratique, nous détaillons les éléments suivants :

-   Les meilleures pratiques de hello est
-   Raison pour laquelle vous souhaitez tooenable que les meilleures pratiques
-   Ce que peut être le résultat de hello si vous ne parvenez pas la meilleure pratique de tooenable hello
-   Comment vous pouvez apprendre tooenable hello il est recommandé

Cet article de meilleures pratiques de la sécurité de base de données Azure est basé sur un avis de consensus et les fonctionnalités de la plateforme Azure et des jeux de fonctionnalités telles qu’elles existent au moment de hello que cet article a été écrit. Avis et les technologies changent au fil du temps et de cet article sera mis à jour sur un tooreflect régulièrement ces modifications.

Les meilleures pratiques en matière de sécurité pour les bases de données Azure qui sont abordées dans le cadre de cet article sont les suivantes :

-   Utilisez le pare-feu règles toorestrict de base de données access
-   Activer l’authentification pour les bases de données
-   Protéger vos données à l’aide du chiffrement
-   Protection des données en transit
-   Activer l’audit pour les bases de données
-   Activer la détection des menaces pour les bases de données


## <a name="use-firewall-rules-toorestrict-database-access"></a>Utilisez le pare-feu règles toorestrict de base de données access

Microsoft Azure SQL Database fournit un service de base de données relationnelle pour Azure et d’autres applications basées sur Internet. sécurité d’accès tooprovide, base de données SQL contrôle l’accès avec les règles de pare-feu limitant la connectivité par adresse IP, les mécanismes d’authentification nécessitant des utilisateurs tooprove leur identité et les mécanismes d’autorisation limitant les actions de toospecific les utilisateurs et les données. Les pare-feu empêchent le serveur de base de données de tous les accès tooyour jusqu'à ce que vous spécifiez les ordinateurs sur lesquels l’autorisation. les pare-feu Hello accorde toodatabases d’accès basé sur hello adresse IP de chaque demande d’origine.

![Règles de pare-feu](./media/azure-database-security-best-practices/azure-database-security-best-practices-Fig1.png)

Hello service de base de données SQL Azure est disponible uniquement via le port TCP 1433. tooaccess une base de données SQL à partir de votre ordinateur, vérifiez que le pare-feu de votre ordinateur client autorise les communications TCP sortantes sur le port TCP 1433. Si elles ne sont pas nécessaires pour les autres applications, bloquez les connexions entrantes sur le port TCP 1433 à l’aide de règles de pare-feu.

Dans le cadre du processus de connexion hello, connexions à partir de machines virtuelles sont des adresses IP différentes tooa redirigé et port unique pour chaque rôle de travail. numéro de port Hello est comprise de hello too11999 11000. Pour plus d’informations sur les ports TCP, consultez [Ports au-delà de 1433 pour ADO.NET 4.5 et SQL Database2](https://docs.microsoft.com/azure/sql-database/sql-database-develop-direct-route-ports-adonet-v12).

> [!Note]
> Pour en savoir plus sur les règles de pare-feu dans la base de données SQL, voir [Règles de pare-feu de la base de données SQL](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).

## <a name="enable-database-authentication"></a>Activer l’authentification pour les bases de données
SQL Database prend en charge deux types d’authentification : l’authentification SQL et l’authentification Azure Active Directory (Azure AD Authentication).

**L’authentification SQL** est recommandée dans les cas suivants :

-   Il permet les environnements toosupport SQL Azure avec des systèmes d’exploitation mixtes, où tous les utilisateurs ne sont pas authentifiés par un domaine Windows.
-   Autorise les applications plus anciennes de SQL Azure toosupport et les applications tierces qui requièrent l’authentification SQL Server.
-   Permet de tooconnect les utilisateurs à partir de domaines inconnus ou non fiables. Par exemple, une application où les clients établis se connectent avec le statut connexions SQL Server tooreceive hello de leurs commandes.
-   Permet à SQL Azure toosupport des applications Web où les utilisateurs créent leurs propres identités.
-   Permet aux logiciels toodistribute développeurs leurs applications à l’aide d’une hiérarchie d’autorisations complexe basées sur connu, présélection des connexions SQL Server.

> [!Note]
> Toutefois, l’authentification SQL Server ne peut pas utiliser le protocole de sécurité Kerberos.

Si vous utilisez **l’authentification SQL** vous devez :

-   Gérer les informations d’identification fortes hello vous-même.
-   Protéger les informations d’identification hello dans la chaîne de connexion hello.
-   Protéger les informations d’identification de hello transmises sur le réseau de hello à partir de la base de données toohello hello Web server (éventuellement). Pour plus d’informations, consultez [Comment : se connecter tooSQL serveur à l’aide de l’authentification SQL dans ASP.NET 2.0](https://msdn.microsoft.com/library/ms998300.aspx).

**L’authentification Active Directory Azure** est un mécanisme de connexion de base de données SQL Azure de tooMicrosoft et [SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-what-is) à l’aide des identités dans Azure Active Directory (Azure AD). Avec l’authentification Azure AD, vous pouvez gérer de manière centralisée les identités hello d’utilisateurs de base de données et d’autres services de Microsoft dans un emplacement central. Gestion des ID fournit un emplacement unique aux utilisateurs de base de données de toomanage et simplifie la gestion de l’autorisation. Avantages hello suivants :

-   Il fournit une authentification de serveur alternatif tooSQL.
-   Vous aide à arrêter la prolifération hello des identités des utilisateurs sur les serveurs de base de données.
-   Permet une rotation du mot de passe dans un emplacement unique.
-   Les clients peuvent gérer les autorisations de base de données à l’aide de groupes (AAD) externes.
-   Il peut éliminer le stockage des mots de passe en activant l’authentification intégrée Windows et les autres formes d’authentification prises en charge par Azure Active Directory.
-   L’authentification Azure AD utilise la relation contenant-contenu de la base de données utilisateurs tooauthenticate identités au niveau de base de données hello.
-   Azure AD prend en charge l’authentification basée sur le jeton pour les applications qui se connectent tooSQL de base de données.
-   L’authentification Azure AD prend en charge ADFS (fédération de domaine) ou l’authentification utilisateur natif/mot de passe pour un répertoire Azure Active Directory local sans synchronisation du domaine.
-   Azure AD prend en charge les connexions à partir de SQL Server Management Studio qui utilisent l’authentification universelle Active Directory, et notamment Multi-Factor Authentication (MFA). MFA comprend une authentification forte avec une gamme d’options de vérification simples (appel téléphonique, SMS, cartes à puce avec code PIN ou notification d’application mobile). Pour plus d’informations, voir [Prise en charge de SSMS pour Azure AD MFA avec la base de données SQL et SQL Data Warehouse](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).

étapes de configuration Hello incluent hello suivant les procédures tooconfigure et utilisent l’authentification Azure Active Directory.

-   Créer et renseigner Azure AD.
-   Associer facultatif : Ou modifier hello active directory qui est associé à votre abonnement Azure.
-   Créer un administrateur Azure Active Directory pour le serveur Azure SQL Server ou pour [Azure SQL Data Warehouse](https://azure.microsoft.com/services/sql-data-warehouse/).
- Configurer vos ordinateurs clients.
-   Créer des utilisateurs de base de données dans votre base de données mappée de tooAzure identités AD.
-   Se connecter tooyour de base de données à l’aide d’identités Azure AD.

Vous trouverez des informations détaillées [ici](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).

## <a name="protect-your-data-using-encryption"></a>Protéger vos données à l’aide du chiffrement

[Chiffrement de données transparent de base de données SQL Azure (TDE)](https://msdn.microsoft.com/library/dn948096.aspx) améliore la protection contre les menaces hello d’activités malveillantes en effectuant le chiffrement en temps réel et déchiffrement de base de données hello, les sauvegardes associées, et les fichiers journaux des transactions au repos sans exiger des modifications toohello application. Stockage hello d’une base de données entière est chiffré à l’aide d’une clé de chiffrement de base de données hello appelée de clé symétrique.

Même lorsque le stockage dans son intégralité hello est chiffré, il est très important tooalso chiffrer votre base de données. Il s’agit d’une implémentation de hello approche défense en profondeur pour la protection des données. Si vous utilisez une base de données SQL Azure et que vous souhaitez tooprotect les données sensibles telles que la carte de crédit ou des numéros de sécurité sociale, vous pouvez chiffrer les bases de données avec chiffrement FIPS 140-2 validé 256 bits AES qui répond aux exigences de hello de nombreuses normes (par exemple, HIPAA, PCI).

Il est important de toounderstand fichiers liés trop[extension du pool () de la mémoire tampon](https://docs.microsoft.com/sql/database-engine/configure-windows/buffer-pool-extension) ne sont pas chiffrés lorsqu’une base de données est chiffrée à l’aide du chiffrement transparent des données. Vous devez utiliser les outils de chiffrement au niveau du système de fichiers tels que [BitLocker](https://technet.microsoft.com/library/cc732774) ou hello [le système EFS (ENCRYPTING File System)](https://technet.microsoft.com/library/cc700811.aspx) pour BPE les fichiers associés.

Depuis un utilisateur autorisé comme un administrateur de sécurité ou un administrateur de base de données peut accéder aux données de hello même si la base de données hello est chiffré avec chiffrement transparent des données, vous devez également suivre les recommandations hello ci-dessous :

-   Activer l’authentification SQL au niveau de base de données hello.
-   Utilisez Azure AD Authentication à l’aide des [rôles RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is).
-   Les applications et les utilisateurs doivent utiliser des tooauthenticate de comptes distincts. De cette manière, vous pouvez limiter les autorisations hello accordées toousers et des applications et réduire les risques de hello d’une activité malveillante.
-   Implémenter la sécurité au niveau de la base de données à l’aide des rôles de base de données fixe (par exemple, db_datareader ou db_datawriter), ou vous pouvez créer des rôles personnalisés pour votre application de toogrant objets de base de données tooselected autorisations explicites.

Pour les autres façons tooencrypt vos données, envisagez de :

-   [Le chiffrement au niveau des cellules](https://msdn.microsoft.com/library/ms179331.aspx) tooencrypt des colonnes spécifiques ou même les cellules de données avec des clés de chiffrement différente.
-   Chiffrement en cours d’utilisation à l’aide d’Always Encrypted : [Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx) autorise les clients tooencrypt des données sensibles dans des applications clientes et de ne jamais révèlent toohello de clés de chiffrement hello du moteur de base de données (base de données SQL ou SQL Server). Par conséquent, la Always Encrypted fournit une séparation entre ceux qui possèdent des données de salutation (et peuvent les afficher) et ceux qui les gèrent les données de salutation (mais ne doivent avoir aucun accès).
-   À l’aide de la sécurité au niveau de la ligne : la sécurité au niveau des lignes permet de clients toocontrol accès toorows dans une table de base de données en fonction des caractéristiques de hello d’utilisateur hello l’exécution d’une requête (par exemple, groupe d’appartenance ou contexte d’exécution). Pour plus d’informations, consultez [Sécurité au niveau des lignes](https://msdn.microsoft.com/library/dn765131).

## <a name="protect-data-in-transit"></a>Protection des données en transit
La protection des données en transit doit être un aspect essentiel de votre stratégie de protection des données. Étant donné que les données allez déplacer dans les deux sens à partir de nombreux emplacements, recommandation générale de hello est toujours utiliser des données de tooexchange protocoles SSL/TLS sur les différents sites. Dans certains cas, vous souhaiterez peut-être canal de communication entière tooisolate hello entre vos locaux et le cloud infrastructure à l’aide d’un réseau privé virtuel (VPN).

Pour les données qui transitent entre votre infrastructure locale et Azure, vous devez envisager le recours aux dispositifs de protection appropriés, comme HTTPS ou VPN.

Pour les organisations qui ont besoin d’accéder toosecure à partir de plusieurs tooAzure locaux de stations de travail, utilisez [VPN de site à site Azure](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-site-to-site-create).

Pour les organisations qui souhaitent utiliser toosecure accès à partir de stations de travail individuelles situées sur site ou hors site tooAzure, envisagez d’utiliser [Point-to-Site VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-point-to-site-create).

Les jeux de données volumineux peuvent être transmis par le biais d’une liaison réseau étendu haut débit dédiée, comme [ExpressRoute](https://azure.microsoft.com/services/expressroute/). Si vous choisissez toouse ExpressRoute, vous pouvez également chiffrer les données de salutation à l’aide de niveau application hello [SSL/TLS](https://support.microsoft.com/kb/257591) ou d’autres protocoles pour une protection supplémentaire.

Si vous interagissez avec le stockage Azure via hello portail Azure, toutes les transactions se produisent via HTTPS. [API REST de stockage](https://msdn.microsoft.com/library/azure/dd179355.aspx) via le protocole HTTPS peut également être utilisé toointeract avec [Azure Storage](https://azure.microsoft.com/services/storage/) et [base de données SQL Azure](https://azure.microsoft.com/services/sql-database/).

Les organisations qui échouent tooprotect des données en transit sont plus vulnérables pour [man in the middle attaques](https://technet.microsoft.com/library/gg195821.aspx), [espionnage](https://technet.microsoft.com/library/gg195641.aspx) et le piratage de session. Ces attaques peuvent être hello première étape de pouvoir accéder aux données de tooconfidential.

toolearn plus en détail l’option VPN Azure, lisez l’article de hello [planification et conception pour la passerelle VPN](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-plan-design).

## <a name="enable-database-auditing"></a>Activer l’audit pour les bases de données
L’audit d’une instance de hello du moteur de base de données SQL Server ou une base de données individuelle implique le suivi et l’enregistrement des événements qui se produisent sur hello du moteur de base de données. L’audit SQL Server vous permet de créer des audits de serveur, qui peuvent contenir des spécifications d’audit de serveur pour les événements au niveau du serveur et des spécifications d’audit de base de données pour les événements au niveau de la base de données. Les événements audités peuvent être écrits toohello les journaux des événements ou des fichiers de tooaudit.

Il existe plusieurs niveaux d’audit pour SQL Server, en fonction des exigences normatives ou gouvernementales de votre installation. SQL Server Audit fournit les outils hello et processus nécessaires tooenable, store et afficher les audits sur différents objets serveur et base de données.

[Audit de base de données SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-auditing) effectue le suivi des événements de base de données et les écrit le journal d’audit de tooan dans votre compte de stockage Azure.

L’audit peut vous aider à respecter une conformité réglementaire, à comprendre l’activité de la base de données et à découvrir des discordances et anomalies susceptibles d’indiquer des problèmes pour l’entreprise ou des violations de la sécurité.

L’audit permet et facilite les normes de conformité toocompliance mais ne garantit pas la conformité.

toolearn plus d’informations sur l’audit de base de données et comment tooenable, lisez l’article de hello [activer la détection des menaces et de l’audit sur les serveurs SQL Server dans le centre de sécurité Azure](https://docs.microsoft.com/azure/security-center/security-center-enable-auditing-on-sql-servers).

## <a name="enable-database-threat-detection"></a>Activer la détection des menaces pour les bases de données
Détection des menaces SQL vous permet de toodetect et répondre toopotential menaces qu’ils se produisent en fournissant des alertes de sécurité sur les activités anormales. Vous recevrez une alerte en cas d’activités de base de données suspectes, de vulnérabilités potentielles, d’attaques par injection de code SQL et de modèles d’accès anormaux à la base de données. Alertes de détection des menaces SQL fournissent des détails d’activité suspecte et recommandent la mesure sur la façon de tooinvestigate et d’atténuer les menaces de hello.

Par exemple, injection SQL est un des hello Web application problèmes de sécurité courants sur hello Internet, les applications utilisées tooattack piloté par les données. Les attaquants profiter d’application vulnérabilités tooinject des instructions SQL malveillantes dans les champs d’entrée application, violation ou modification des données dans la base de données hello.

toolearn comment tooset la détection des menaces pour votre base de données Bonjour Azure, consultez portail [la détection des menaces de base de données SQL](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection).

De plus, la détection des menaces SQL intègre des alertes avec [Azure Security Center](https://azure.microsoft.com/services/security-center/). Nous vous invitons tootry son évolution horizontale pendant 60 jours pour le libérer.

toolearn plus d’informations sur la détection des menaces de base de données et comment tooenable, lisez l’article de hello [activer la détection des menaces et de l’audit sur les serveurs SQL Server dans le centre de sécurité Azure](https://docs.microsoft.com/azure/security-center/security-center-enable-auditing-on-sql-servers).

## <a name="conclusion"></a>Conclusion
Azure Database est une plateforme robuste de base de données, avec un éventail complet de fonctionnalités de sécurité qui répondent à de nombreuses exigences en matière de conformité réglementaire et organisationnelles. Vous pouvez protéger les données en contrôlant les données de tooyour hello accès physique et à l’aide de diverses options de sécurité des données à hello fichier, colonne ou au niveau des lignes avec chiffrement Transparent des données, le chiffrement au niveau des cellules ou sécurité de niveau ligne. Toujours chiffré permet également des opérations sur les données chiffrées, ce qui simplifie le processus hello des mises à jour de l’application. À son tour, journaux tooauditing d’accès de l’activité de la base de données SQL fournit des informations de hello vous avez besoin, ce qui vous tooknow comment et quand les données sont accessibles.

## <a name="next-steps"></a>Étapes suivantes
- toolearn en savoir plus sur les règles de pare-feu, consultez [des règles de pare-feu](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).
- toolearn sur les utilisateurs et les connexions, consultez [gérer des connexions](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins).
- Pour obtenir un didacticiel, consultez [Sécuriser votre base de données Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-security-tutorial).
