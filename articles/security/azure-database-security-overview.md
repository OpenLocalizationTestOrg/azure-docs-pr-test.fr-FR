---
title: "Présentation de la sécurité de base de données aaaAzure | Documents Microsoft"
description: "Cet article fournit une vue d’ensemble des fonctionnalités de sécurité de base de données Azure hello."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: TomSh
ms.openlocfilehash: 13f14b99d15800e85e9906a9d167eb0adf2135de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-security-overview"></a>Vue d’ensemble de la sécurité des bases de données Azure

La sécurité est une préoccupation majeure lors de la gestion de bases de données, et elle a toujours été une priorité pour Azure SQL Database. Azure SQL Database prend en charge la sécurité de connexion avec des règles de pare-feu et un chiffrement de connexion. Il prend en charge l’authentification avec nom d’utilisateur et mot de passe, ainsi que l’authentification Azure Active Directory qui utilise des identités gérées par Azure Active Directory. L’autorisation utilise le contrôle d’accès en fonction du rôle.

Base de données SQL Azure prend en charge le chiffrement en effectuant le chiffrement en temps réel et le déchiffrement des bases de données, les sauvegardes associées et les fichiers journaux des transactions au repos sans nécessiter de modifications toohello application.

Microsoft fournit des données d’entreprise tooencrypt autres façons :

-   Au niveau des cellules des colonnes spécifiques de chiffrement tooencrypt ou même les cellules de données avec des clés de chiffrement différente.
-   S’il vous faut un module de sécurité matériel ou si vous devez gérer la hiérarchie des clés de chiffrement de manière centralisée, consultez l’article de blog relatif à l’utilisation d’Azure Key Vault avec SQL Server dans une machine virtuelle Azure.
-   Toujours chiffré (actuellement en version préliminaire) rend tooapplications transparent de chiffrement et permet aux clients tooencrypt des données sensibles dans des applications clientes sans partager les clés de chiffrement hello avec la base de données SQL.

Audit de base de données SQL Azure permet aux entreprises toorecord événements tooan audit login le stockage Azure. L’audit de base de données SQL intègre également des analyses et des rapports détaillés de toofacilitate Microsoft Power BI.

 Bases de données SQL Azure peuvent être parfaitement sécurisé toosatisfy plus réglementaire ou des exigences de sécurité, notamment HIPAA et PCI DSS niveau 1, ISO 27001/27002. Liste actuelle des certifications de conformité de sécurité est disponible à l’adresse hello [site de Microsoft Azure Trust Center](http://azure.microsoft.com/support/trust-center/services/).

Cet article explique les principes fondamentaux de hello de sécurisation des bases de données SQL Microsoft Azure pour structuré, tabulaires et les données relationnelles. Plus spécifiquement, cet article vous offre un aperçu sur les ressources dédiées à la protection des données, au contrôle d’accès et à la surveillance proactive.

Cet article de présentation de la sécurité de base de données Azure se concentre sur hello suivant de zones :

-   Protection des données
-   Contrôle d’accès
-   Surveillance proactive
-   Gestion centralisée de la sécurité
-   Place de marché Azure

## <a name="protect-data"></a>Protection des données

SQL Database sécurise vos données grâce au chiffrement : il utilise [Transport Layer Security](https://support.microsoft.com/kb/3135244) pour les données en mouvement, [Transparent Data Encryption](http://go.microsoft.com/fwlink/?LinkId=526242) pour les données au repos et [Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx) pour les données en cours d’utilisation.

Dans cette section, nous parlons de :

-   Chiffrement en mouvement
-   Chiffrement au repos
-   Chiffrement en cours d’utilisation (client)

Pour les autres façons tooencrypt vos données, envisagez de :

-   [Le chiffrement au niveau des cellules](https://msdn.microsoft.com/library/ms179331.aspx) tooencrypt des colonnes spécifiques ou même les cellules de données avec des clés de chiffrement différente.
-   S’il vous faut un module de sécurité matériel ou si vous devez gérer la hiérarchie des clés de chiffrement de manière centralisée, consultez l’article de blog relatif au [coffre de clés Microsoft Azure avec SQL Server dans une machine virtuelle Azure](http://blogs.technet.com/b/kv/archive/2015/01/12/using-the-key-vault-for-sql-server-encryption.aspx).

### <a name="encryption-in-motion"></a>Chiffrement en mouvement

Un problème courant pour toutes les applications client/serveur est nécessaire hello confidentialité déplacent les données sur les réseaux publics et privés. Si le déplacement d’un réseau de données ne sont pas chiffrées, est chance hello peuvent être capturée et vol par les utilisateurs non autorisés. Lorsque vous traitez des services de base de données, vous devez toomake assurer que les données sont chiffrées entre hello de base de données client et serveur, ainsi qu’entre les serveurs de base de données qui communiquent entre eux et avec les applications de couche intermédiaire.

Un problème lorsque vous administrez un réseau est la sécurisation des données échangées entre les applications via un réseau non approuvé. Vous pouvez utiliser [TLS/SSL](https://docs.microsoft.com/windows-server/security/tls/transport-layer-security-protocol) tooauthenticate serveurs et clients, puis l’utiliser tooencrypt des messages entre les parties hello authentifié.

Dans le processus d’authentification hello, un client TLS/SSL envoie un message tooa TLS/SSL serveur et serveur de hello répond avec les informations de hello tooauthenticate lui-même a besoin de ce serveur hello. hello client et serveur effectuent un échange supplémentaire de clés de session et hello fin de dialogue d’authentification. Lorsque l’authentification est terminée, les communications SSL sécurisées peuvent commencer entre les serveur hello et client hello à l’aide de clés de chiffrement symétriques hello établies pendant le processus d’authentification hello.

Toutes les connexions tooAzure base de données SQL exiger le chiffrement (SSL/TLS) à toutes les heures pendant tooand « en transit » à partir de la base de données hello des données. SQL Azure utilise des clients et serveurs tooauthenticate TLS/SSL et l’utiliser tooencrypt des messages entre les parties hello authentifié. Dans la chaîne de connexion de votre application, vous devez spécifier une connexion de paramètres tooencrypt hello et pas tootrust hello certificat de serveur (cela est fait pour vous si vous copiez votre chaîne de connexion hors hello portail classique Azure), sinon hello va de connexion ne vérifie pas identité hello du serveur de hello et sont susceptibles d’être trop « man-in-the-middle » attaques. Pour hello pilote ADO.NET, par exemple, ces paramètres de chaîne de connexion Encrypt = True et TrustServerCertificate = False.

### <a name="encryption-at-rest"></a>Chiffrement au repos
Vous pouvez prendre plusieurs précautions toohelp hello sécurisé de base de données telles que la conception d’un système sécurisé, chiffrer les ressources confidentielles et créer un pare-feu autour des serveurs de base de données hello. Toutefois, dans un scénario où hello le support physique (par exemple, les lecteurs ou les bandes de sauvegarde) est dérobé, une personne malveillante peut simplement restaurer ou attacher la base de données hello et parcourir les données de salutation.

Une solution tooencrypt hello des données sensibles dans la base de données hello et protège les clés hello qui sont des données de hello tooencrypt utilisé avec un certificat. Cela empêche toute personne sans les clés hello à l’aide des données de hello, mais ce type de protection doit être planifié.

toosolve ce problème, SQL Server et SQL Azure prend en charge [Transparent Data Encryption (TDE)](https://docs.microsoft.com/sql/relational-databases/securityrecryption/transparent-data-encryption-tde). La fonctionnalité Transparent Data Encryption chiffre les fichiers de données SQL Server et Azure SQL Database. Il s’agit de ce qu’on appelle le chiffrement de données au repos.

Le chiffrement transparent des données de la base de données SQL Azure permet de protéger contre les menaces hello d’activités malveillantes en effectuant le chiffrement en temps réel et le déchiffrement de la base de données de hello, les sauvegardes associées et les fichiers journaux des transactions au repos sans nécessiter de modifications application toohello.  

Stockage hello d’une base de données entière est chiffré à l’aide d’une clé de chiffrement de base de données hello appelée de clé symétrique. Dans la base de données SQL, la clé de chiffrement de base de données hello est protégé par un certificat de serveur intégré. certificat de serveur intégré Hello est unique pour chaque serveur de base de données SQL.

Si une base de données est dans un relation GeoDR, elle est protégée par une clé différente sur chaque serveur. Si les deux bases de données sont connecté toohello même serveur, elles partagent hello même certificat intégré. Microsoft alterne automatiquement ces certificats au moins tous les 90 jours. Pour obtenir une description générale du chiffrement transparent des données, consultez [Chiffrement transparent des données (TDE)](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-tde).

### <a name="encryption-in-use-client"></a>Chiffrement en cours d’utilisation (client)

La plupart des violations de données impliquant un vol hello de données critiques telles que les numéros de carte de crédit ou des informations d’identification personnelle. Les bases de données peuvent contenir des trésors d’informations sensibles. Ils peuvent contenir des données personnelles de clients, des informations confidentielles sur la concurrence et des éléments de propriété intellectuelle. Les pertes ou vols de données, en particulier de données client, peuvent entraîner une dégradation de l’image de marque, un déficit de compétitivité, des amendes lourdes, voire des actions en justice.

![Toujours chiffré](./media/azure-databse-security-overview/azure-database-fig1.png)

[Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx) est une fonctionnalité conçue tooprotect les données sensibles, telles que les numéros de carte de crédit ou nationaux d’identification (par exemple, États-Unis numéros de sécurité sociale), stockées dans les bases de données de base de données SQL Azure ou SQL Server. Always Encrypted permet aux clients tooencrypt des données sensibles dans des applications clientes et ne jamais révéler toohello de clés de chiffrement hello du moteur de base de données (base de données SQL ou SQL Server).

Always Encrypted fournit une séparation entre ceux qui possèdent des données de salutation (et peuvent les afficher) et ceux qui les gèrent les données de salutation (mais ne doivent avoir aucun accès). En s’assurant que les administrateurs de base de données locaux, les opérateurs de base de données cloud ou d’autres privilèges élevés, mais les utilisateurs non autorisés, ne peut pas accéder à des données chiffrée de hello,

En outre, Always Encrypted rend tooapplications transparent de chiffrement. Un pilote de chiffrement intégral installé sur l’ordinateur client de hello afin qu’il peut chiffrer et déchiffrer les données sensibles dans une application cliente de hello automatiquement. Hello pilote chiffre les données de hello dans les colonnes sensibles avant de les transmettre hello toohello de données du moteur de base de données et il réécrit automatiquement les requêtes afin que l’application de toohello hello sémantique sont conservés. De même, hello en toute transparence déchiffre les données stockées dans des colonnes de base de données chiffrées contenues dans les résultats de la requête.

## <a name="access-control"></a>Contrôle d’accès
sécurité tooprovide, base de données SQL contrôle l’accès avec les règles de pare-feu limitant la connectivité par adresse IP, les mécanismes d’authentification nécessitant des utilisateurs tooprove leur identité et les mécanismes d’autorisation limitant les actions de toospecific les utilisateurs et les données.

### <a name="database-access"></a>Accès à la base de données

Protection des données commence à contrôler l’accès aux données de tooyour. Hello de centre de données qui héberge vos données gère l’accès physique, vous pouvez configurer une pare-feu toomanage sécurité au niveau de la couche réseau hello. Vous pouvez également contrôler l’accès en configurant des connexions pour l’authentification, et définir des autorisations pour les rôles serveur et base de données.

Dans cette section, nous parlons de :

-   Pare-feu et règles de pare-feu
-   Authentification
-   Autorisation

#### <a name="firewall-and-firewall-rules"></a>Pare-feu et règles de pare-feu

Microsoft Azure SQL Database fournit un service de base de données relationnelle pour Azure et d’autres applications basées sur Internet. toohelp protéger vos données, les pare-feu empêchent le serveur de base de données de tous les accès tooyour jusqu'à ce que vous spécifiez les ordinateurs sur lesquels l’autorisation. les pare-feu Hello accorde toodatabases d’accès basé sur hello adresse IP de chaque demande d’origine. Pour plus d’informations, consultez l’article [Vue d’ensemble des règles de pare-feu d’Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).

Hello [base de données SQL Azure](https://azure.microsoft.com/services/sql-database/) service est disponible uniquement via le port TCP 1433. tooaccess une base de données SQL à partir de votre ordinateur, vérifiez que le pare-feu de votre ordinateur client autorise les communications TCP sortantes sur le port TCP 1433. Si elles ne sont pas nécessaire pour les autres applications, bloquez les connexions entrantes sur le port TCP 1433.

#### <a name="authentication"></a>Authentification

L’authentification de base de données SQL fait référence à toohow vous prouver votre identité lors de la connexion de base de données toohello. Une base de données SQL prend en charge deux types d’authentification :

-   **L’authentification SQL :** un seul compte de connexion est créé lorsqu’une instance SQL logique est créée, appelée hello compte abonné de base de données SQL. Ce compte se connecte en utilisant l’[Authentification SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview) (nom d’utilisateur et mot de passe). Ce compte est qu'un administrateur sur l’instance de serveur logique hello et sur toutes les bases de données utilisateur attaché toothat instance. autorisations Hello Hello compte de l’abonné ne peut pas être limitées. Un seul de ces comptes peut exister.
-   **Authentification Active Directory Azure :** [l’authentification Azure Active Directory](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication) est un mécanisme de connexion tooMicrosoft base de données SQL Azure et SQL Data Warehouse à l’aide des identités dans Azure Active Directory () Azure AD). Cela permet de vous toocentrally gérer les identités des utilisateurs de base de données.

![Authentification](./media/azure-databse-security-overview/azure-database-fig2.png)

 Avantages de l’authentification Azure Active Directory :
  - Il fournit une authentification de serveur alternatif tooSQL.
  - Aussi, il permet d’arrêter la prolifération de hello des identités des utilisateurs sur les serveurs de base de données & permet la rotation de mot de passe dans un emplacement unique.
  - Vous pouvez gérer les autorisations de base de données à l’aide de groupes (Azure Active Directory) externes.
  - Il peut éliminer le stockage des mots de passe en activant l’authentification intégrée Windows et les autres formes d’authentification prises en charge par Azure Active Directory.

#### <a name="authorization"></a>Autorisation
[Autorisation](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins) fait référence toowhat un utilisateur peut faire au sein d’une base de données SQL Azure, et cela est contrôlé par la base de données de votre compte utilisateur [appartenances au rôle](https://msdn.microsoft.com/library/ms189121) et [autorisations au niveau de l’objet](https://msdn.microsoft.com/library/ms191291.aspx). Autorisation est processus hello permettant de déterminer les ressources sécurisables auxquelles une entité de sécurité peut accéder et les opérations qui sont autorisées pour ces ressources.

### <a name="application-access"></a>Accès aux applications

Dans cette section, nous parlons de :

-   Masquage des données dynamiques
-   Sécurité au niveau des lignes

#### <a name="dynamic-data-masking"></a>Masquage des données dynamiques
Un représentant du service à un centre d’appels peut identifier des appelants par quelques chiffres de leur numéro de carte de crédit ou le numéro de sécurité sociale, mais ces éléments ne doivent pas être entièrement les données exposées toohello représentant du service.

Une règle de masquage peut être définie que tous les masques de mais hello les quatre derniers chiffres d’un numéro de carte de crédit hello jeu de résultats d’une requête ou un numéro de sécurité sociale.

![Masquage des données dynamiques](./media/azure-databse-security-overview/azure-database-fig3.png)

Autre exemple, un masque de données approprié peut être défini tooprotect informations d’identification personnelle (PII) données, afin qu’un développeur peut interroger les environnements de production aux fins de dépannage sans violer les réglementations de conformité.

[Base de données dynamique masquage des données SQL](https://docs.microsoft.com/azure/sql-database/sql-database-dynamic-data-masking-get-started) limite l’exposition des données sensibles en les masquant aux utilisateurs privilèges toonon. Masquage dynamique des données sont prise en charge pour la version V12 de hello de base de données SQL Azure.

[Masquage dynamique des données](https://docs.microsoft.com/sql/relational-databases/security/dynamic-data-masking) vous aide à empêcher les données toosensitive de tout accès non autorisé vous toodesignate la quantité de tooreveal des données sensibles hello avec un impact minimal sur la couche d’application hello. Il s’agit d’une fonctionnalité basée sur des stratégies de sécurité qui masque les données sensibles hello hello jeu de résultats d’une requête sur des champs de base de données désignée données hello hello de base de données ne sont pas modifiées.


> [!Note]
> Masquage dynamique des données peuvent être configuré par l’administrateur de base de données Azure hello, un administrateur de serveur ou des rôles de responsable de la sécurité.

#### <a name="row-level-security"></a>Sécurité au niveau des lignes
Une autre exigence de sécurité courante pour les bases de données mutualisées est la [Sécurité au niveau des lignes](https://msdn.microsoft.com/library/dn765131.aspx). Cette fonctionnalité vous permet de toorows d’accès toocontrol dans une table de base de données en fonction des caractéristiques de hello d’utilisateur hello l’exécution d’une requête (par exemple, groupe d’appartenance ou contexte d’exécution).

![Sécurité au niveau des lignes](./media/azure-databse-security-overview/azure-database-fig4.png)

logique de restriction d’accès Hello est située dans la couche de base de données hello plutôt que loin des données hello dans une autre couche application. système de base de données Hello applique des restrictions d’accès de hello chaque fois que cet accès aux données est tenté à partir de n’importe quel niveau. Cela rend votre système de sécurité plus fiable et plus robuste, en réduisant la surface d’exposition de hello de votre système de sécurité.

La sécurité au niveau des lignes introduit le contrôle d’accès en fonction d’un prédicat. Elle propose une évaluation flexible, centralisée et basée sur un prédicat qui peut prendre en compte les métadonnées ou tout autre critère hello administrateur détermine comme appropriée. prédicat de Hello est utilisé comme un critère toodetermine utilisateur de hello a des données de toohello hello accès approprié en fonction des attributs de l’utilisateur ou non. Un contrôle d’accès en fonction d’une étiquette peut être implémenté en utilisant un contrôle d’accès en fonction d’un prédicat.

## <a name="proactive-monitoring"></a>Surveillance proactive
SQL Database sécurise vos données en fournissant des fonctionnalités d’**audit** et de **détection des menaces**.

### <a name="auditing"></a>Audit
L’audit de base de données SQL augmente votre capacité toogain connaître les événements et les modifications qui se produisent dans la base de données hello, y compris les mises à jour et les requêtes sur les données de salutation.

[Audit de base de données SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-auditing-get-started) effectue le suivi des événements de base de données et les écrit le journal d’audit de tooan dans votre compte de stockage Azure. L’audit peut vous aider à respecter une conformité réglementaire, à comprendre l’activité de la base de données et à découvrir des discordances et anomalies susceptibles d’indiquer des problèmes pour l’entreprise ou des violations de la sécurité. L’audit permet et facilite les normes de conformité toocompliance mais ne garantit pas la conformité.

L’audit de bases de données SQL permet :

-   **La rétention** d’une piste d’audit d’événements sélectionnés. Vous pouvez définir des catégories de base de données actions toobe est auditée.
-   **La génération de rapports** sur les activités de la base de données. Vous pouvez utiliser les rapports préconfigurés et un tooget de tableau de bord rapidement opérationnel avec activité et les rapports d’événements.
-   **L'analyse** des rapports. Vous pouvez repérer les événements suspects, les activités inhabituelles et les tendances.

Il existe deux méthodes d’audit :

-   **L’audit des objets BLOB** -dans les journaux tooAzure stockage d’objets Blob. Il s’agit d’une méthode d’audit plus récente, qui fournit des performances plus élevées, prend en charge l’audit avec une granularité plus élevée au niveau des objets et est plus économique.
-   **Table d’audit** -tooAzure le stockage de Table les journaux sont écrits.

### <a name="threat-detection"></a>Détection de menaces
La [détection des menaces Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection) détecte des activités suspectes indiquant des menaces de sécurité potentielles. La détection des menaces vous permet de toorespond toosuspicious les événements de base de données hello, telles que les Injections SQL, qu’ils se produisent. Il fournit des alertes et autorise l’utilisation de hello de tooexplore de l’audit de base de données SQL Azure d’événements suspects hello.

![Détection des menaces](./media/azure-databse-security-overview/azure-database-fig5.jpg)

Par exemple, injection SQL est un des hello Web application problèmes de sécurité courants sur hello Internet, les applications utilisées tooattack piloté par les données. Les attaquants profiter d’application vulnérabilités tooinject des instructions SQL malveillantes dans les champs d’entrée application, violation ou modification des données dans la base de données hello.

Les responsables de la sécurité ou autres administrateurs désignés peuvent obtenir une notification immédiate concernant les activités suspectes qui interviennent sur la base de données. Chaque notification fournit des détails d’une activité suspecte hello et recommande comment toofurther examiner et d’atténuer les menaces de hello.        

## <a name="centralized-security-management"></a>Gestion centralisée de la sécurité

[Centre de sécurité Azure](https://azure.microsoft.com/documentation/services/security-center/) vous aide à empêcher, détecter et répondre toothreats. Il fournit une surveillance de la sécurité et une gestion des stratégies intégrées pour l’ensemble de vos abonnements Azure, vous aidant ainsi à détecter les menaces qui pourraient passer inaperçues. De plus, il est compatible avec un vaste écosystème de solutions de sécurité.

[Centre de sécurité](https://docs.microsoft.com/azure/security-center/security-center-sql-database) vous aide à protéger les données dans la base de données SQL en offrant une visibilité sécurité hello de tous vos serveurs et bases de données. Avec Security Center, vous pouvez :

-   définir des stratégies pour l’audit et le chiffrement de SQL Database ;
-   Surveillance de la sécurité hello des ressources de base de données SQL dans tous vos abonnements.
-   identifier et corriger rapidement les problèmes de sécurité ;
-   intégrer les alertes de la [détection de menaces Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection).
-   Le Centre de sécurité prend en charge l’accès en fonction du rôle.

## <a name="azure-marketplace"></a>Azure Marketplace

Bonjour Azure Marketplace est un marketplace d’applications et services en ligne qui permet des clients tooAzure leurs solutions monde hello naissantes et logiciels indépendant (ISV) toooffer.
Bonjour Azure Marketplace combine écosystèmes de partenaires de Microsoft Azure dans un toobetter plate-forme unique et unifiée répondre à nos clients et partenaires. Cliquez sur [ici](https://azuremarketplace.microsoft.com/marketplace/apps?search=Database%20Security&page=1) tooglance produits de sécurité de base de données disponibles sur le marché Azure.

## <a name="next-steps"></a>Étapes suivantes

- En savoir plus sur la manière de [Sécuriser votre base de données SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-security-tutorial).
- En savoir plus sur [Azure Security Center et SQL Database](https://docs.microsoft.com/azure/security-center/security-center-sql-database).
- toolearn en savoir plus sur la détection des menaces, consultez [la détection des menaces de base de données SQL](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection).
- toolearn, voir [performances de base de données SQL d’améliorer](https://docs.microsoft.com/azure/sql-database/sql-database-performance-tutorial). 
