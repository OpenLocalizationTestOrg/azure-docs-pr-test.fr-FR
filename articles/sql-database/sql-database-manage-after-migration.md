---
title: "Gérer après la migration - Azure SQL Database | Microsoft Docs"
description: "Découvrez comment gérer votre base de données après la migration vers Azure SQL Database."
services: sql-database
documentationcenter: 
author: joesackmsft
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: migrate
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Inactive
ms.date: 12/06/2016
ms.author: Joe.Sack
ms.suite: sql
ms.prod_service: sql-database
ms.component: migration
ms.openlocfilehash: b65236fb2d11473d626ee2602237ed4a49380702
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/08/2017
---
# <a name="new-dba-in-the-cloud--managing-your-database-in-azure-sql-database"></a>Nouvel administrateur de base de données dans le cloud – Gestion de votre base de données dans Azure SQL Database

Le passage d’un environnement autogéré et auto-contrôlé traditionnel à un environnement PaaS peut sembler un peu lourd dans un premier temps. En tant que développeur d’applications ou administrateur de base de données, vous avez besoin de connaître les principales fonctionnalités de la plateforme qui facilitent le maintien de la disponibilité, des performances, de la sécurité et de la résilience de votre application, en continu. Cet article va répondre précisément à ce besoin. L’article organise succinctement les ressources et vous fournit des conseils sur la façon de mieux utiliser les fonctionnalités clés de SQL Database pour gérer votre application, maintenir son efficacité et atteindre des résultats optimaux dans le cloud. Cet article vous intéresse si vous êtes dans les cas suivants :
- Vous êtes en train d’évaluer la migration de vos applications vers Azure SQL DB – Modernisation de vos applications.
- Vous êtes en train d’effectuer la migration de vos applications – Scénario de migration en cours.
- Vous avez récemment terminé la migration vers Azure SQL DB – Nouvel administrateur de base de données dans le cloud.

Cet article présente certaines des principales caractéristiques d’Azure SQL Database en tant que plateforme que vous pouvez exploiter dès maintenant. Ces caractéristiques sont les suivantes : 
- Continuité d’activité et récupération d’urgence (BCDR)
- Sécurité et conformité
- Surveillance et maintenance de bases de données intelligentes
- Déplacement des données


## <a name="business-continuity-and-disaster-recovery-bcdr"></a>Continuité d’activité et récupération d’urgence (BCDR)
Les possibilités de continuité d’activité et de récupération d’urgence vous permettent de poursuivre votre activité, comme à l’accoutumée, en cas de sinistre. Un sinistre peut correspondre à un événement au niveau de la base de données (par exemple, une personne supprime par erreur une table essentielle) ou à un événement au niveau du centre de données (catastrophe naturelle dans la région, comme un tsunami par exemple). 

### <a name="how-do-i-create-and-manage-backups-on-sql-database"></a>Comment créer et gérer les sauvegardes dans SQL Database ?
Vous ne créez pas de sauvegardes sur Azure SQL Database parce que vous n’avez pas à le faire. SQL Database sauvegarde automatiquement les bases de données pour vous, donc vous n’avez plus à vous inquiéter de leur planification, leur exécution et leur gestion. La plateforme effectue une sauvegarde complète toutes les semaines, une sauvegarde différentielle à l’issue de quelques heures et une sauvegarde de journal toutes les 5 minutes pour garantir l’efficacité de la récupération d’urgence et une perte de données minimale. La première sauvegarde complète se produit dès que vous créez une base de données. Ces sauvegardes sont à votre disposition pendant un certain temps appelé « période de rétention » qui varie selon le niveau de performance que vous choisissez.  SQL Database vous offre la possibilité d’effectuer une restauration à partir de n’importe quel point dans le temps compris dans cette période de rétention à l’aide d’une [récupération jusqu’à une date et heure](sql-database-recovery-using-backups.md#point-in-time-restore).

|Niveau de performance|Période de rétention en jours|
|---|:---:|
|De base|7|
|Standard|35|
|Premium|35|
|||

De plus, la fonctionnalité de [rétention à long terme](sql-database-long-term-retention.md) vous permet de stocker vos fichiers de sauvegarde pendant une période plus longue, pouvant aller jusqu’à 10 ans, et de restaurer les données de ces sauvegardes à partir de n’importe quel point compris dans cette période. De plus, les sauvegardes de bases de données sont conservées dans un stockage géorépliqué pour assurer leur résilience en cas de catastrophe à l’échelle d’une région. Vous pouvez également restaurer ces sauvegardes dans n’importe quelle région Azure à tout point dans le temps compris dans la période de rétention. Consultez [Vue d’ensemble de la continuité des activités](sql-database-business-continuity.md).

### <a name="how-do-i-ensure-business-continuity-in-the-event-of-a-datacenter-level-disaster-or-regional-catastrophe"></a>Comment faire pour assurer la continuité de l’activité en cas de sinistre au niveau du centre de données ou de catastrophe au niveau d’une région ?
Étant donné que vos sauvegardes de bases de données sont stockées dans un sous-système de stockage géorépliqué, en cas de sinistre régional, vous pouvez restaurer la sauvegarde dans une autre région Azure. Cette fonctionnalité s’appelle la géorestauration. L’objectif de point de récupération (RPO) correspondant est généralement inférieur à 1 heure et le temps de récupération estimé est compris entre quelques minutes et quelques heures.

Pour les bases de données critiques, Azure SQL Database propose une géoréplication active. En bref, une copie secondaire géorépliquée de votre base de données d’origine est créée dans une autre région. Par exemple, votre base de données est initialement hébergée dans la région Azure Ouest des États-Unis et vous avez besoin d’une résilience en cas de sinistre régional. Vous créez alors un géoréplica actif de la base de données de la région Ouest des États-Unis dans la région Est des États-Unis. Quand la catastrophe frappe la région Ouest des États-Unis, vous pouvez basculer vers la région Est des États-Unis. Leur configuration dans un groupe de basculement automatique est préférable, car ce dernier garantit que la base de données peut basculer automatiquement vers le serveur secondaire de la région Est des États-Unis en cas de sinistre. Le RPO correspondant est inférieur à 5 secondes et le temps de récupération estimé est inférieur à 30 secondes.

Si aucun groupe de basculement automatique n’est configuré, votre application doit effectuer une surveillance active et déclencher le basculement vers les bases de données secondaires en cas d’urgence. Vous pouvez créer jusqu’à 4 géoréplicas actifs de ce type dans les différentes régions Azure. Vous obtenez ainsi des résultats encore meilleurs. Vous pouvez également accéder à ces géoréplicas actifs secondaires en lecture seule. Cette possibilité s’avère très pratique pour réduire la latence dans un scénario d’application géodistribuée. 

### <a name="how-does-my-disaster-recovery-plan-change-from-on-premises-to-sql-database"></a>En quoi mon plan de récupération d’urgence local diffère de celui de SQL Database ?
En résumé, le programme d’installation traditionnel de SQL Server local vous obligeait à gérer activement votre disponibilité à l’aide de fonctionnalités comme le clustering de basculement, la mise en miroir de base de données, la réplication transactionnelle, la copie des journaux de transaction, etc. et à assurer la maintenance et la gestion de sauvegardes pour garantir la continuité de l’activité. Avec SQL Database, la plateforme gère tout cela pour vous, donc vous pouvez vous concentrer sur le développement et l’optimisation de votre application de base de données, sans avoir à vous soucier autant de la gestion des sinistres. Vous pouvez avoir des plans de sauvegarde et de récupération d’urgence, configurables et opérationnels en quelques clics seulement par le biais du portail Azure (ou en utilisant quelques commandes des API PowerShell). 

Pour plus d’informations sur la récupération d’urgence, consultez : [Récupération d’urgence Azure SQL Database 101](https://azure.microsoft.com/blog/azure-sql-databases-disaster-recovery-101/)

## <a name="security-and-compliance"></a>Sécurité et conformité
SQL Database prend très au sérieux la sécurité et la confidentialité. La sécurité au sein de SQL Database est disponible au niveau de la base de données et au niveau de la plateforme. Il est plus facile de la comprendre en la classant dans plusieurs couches. Au niveau de chaque couche, vous pouvez contrôler et fournir une sécurité optimale pour votre application. Ces couches sont les suivantes :
- Identité et authentification ([authentification Windows/SQL et authentification Azure Active Directory [AAD]](sql-database-control-access.md)).
- Activité de surveillance ([audit](sql-database-auditing.md) et [détection des menaces](sql-database-threat-detection.md)).
- Protection des données réelles ([Transparent Data Encryption [TDE]](/sql/relational-databases/security/encryption/transparent-data-encryption-azure-sql) et [Always Encrypted [AE]](/sql/relational-databases/security/encryption/always-encrypted-database-engine)). 
- Contrôle de l’accès aux données sensibles et privilégiées ([sécurité au niveau des lignes](/sql/relational-databases/security/row-level-security) et [Dynamic Data Masking](/sql/relational-databases/security/dynamic-data-masking)).

[Azure Security Center](https://azure.microsoft.com/services/security-center/) offre une gestion centralisée de la sécurité pour les charges de travail qui s’exécutent dans Azure, localement et dans d’autres clouds. Vous pouvez voir si les fonctionnalités de protection essentielles de SQL Database, telles que l’[audit](sql-database-auditing.md) et [Transparent Data Encryption [TDE]](/sql/relational-databases/security/encryption/transparent-data-encryption-azure-sql), sont configurées pour toutes les ressources. Si nécessaire, vous pouvez créer des stratégies basées sur vos propres exigences.

### <a name="what-user-authentication-methods-are-offered-in-sql-database"></a>Quelles sont les méthodes d’authentification utilisateur proposées dans SQL Database ?
SQL Database propose [deux méthodes d’authentification](sql-database-control-access.md#authentication) : 
- [Authentification Azure Active Directory](sql-database-aad-authentication.md)
- Authentification SQL 

L’authentification Windows traditionnelle n’est pas prise en charge. Azure Active Directory (AD) est un service centralisé de gestion des identités et des accès. Ce service vous permet de proposer très facilement un accès par authentification unique à tout le personnel de votre organisation. Autrement dit, les informations d’identification sont partagées entre tous les services Azure pour une authentification plus simple. AAD prend en charge [MFA (Multi Factor Authentication)](sql-database-ssms-mfa-authentication.md) et, en [quelques clics](../active-directory/connect/active-directory-aadconnect-get-started-express.md), peut être intégré à Windows Server Active Directory. L’authentification SQL fonctionne exactement comme par le passé. Vous fournissez un nom d’utilisateur/mot de passe et vous pouvez authentifier des utilisateurs après de toute base de données sur un serveur logique donné. Cela permet également à SQL Database et SQL Data Warehouse de proposer une authentification multifacteur et des comptes d’utilisateur Invité dans un domaine Azure AD. Si vous disposez déjà d’Active Directory localement, vous pouvez fédérer l’annuaire avec Azure Active Directory pour étendre votre annuaire à Azure.

|**Si vous…**|**SQL Database/SQL Data Warehouse**|
|---|---|
|Préférez ne pas utiliser Azure Active Directory (AD) dans Azure|Utilisez l’[authentification SQL](sql-database-security-overview.md)|
|Avez utilisé AD avec SQL Server localement|[Fédérez AD avec Azure AD](../active-directory/connect/active-directory-aadconnect.md), puis utilisez l’authentification basée sur Azure AD Authentication. Ainsi, vous pouvez utiliser l’authentification unique.|
|Devez appliquer l’authentification multifacteur via MFA (Multi-Factor Authentication)|Imposez MFA en tant que stratégie via l’[accès conditionnel Microsoft](sql-database-conditional-access.md), et utilisez l’[authentification universelle Azure AD avec prise en charge de MFA](sql-database-ssms-mfa-authentication.md).|
|Avez des comptes Invité issus de comptes Microsoft (live.com, outlook.com) ou d’autres domaines (gmail.com)|Utilisez l’[authentification universelle Azure AD](sql-database-ssms-mfa-authentication.md) de SQL Database/Data Warehouse, qui tire profit d’[Azure AD B2B Collaboration](../active-directory/active-directory-b2b-what-is-azure-ad-b2b.md).|
|Êtes connecté à Windows avec des informations d’identification Azure AD provenant d’un domaine fédéré|Utilisez l’[authentification intégrée Azure AD](sql-database-aad-authentication-configure.md).|
|Êtes connecté à Windows avec des informations d’identification d’un domaine non fédéré avec Azure|Utilisez l’[authentification intégrée Azure AD](sql-database-aad-authentication-configure.md).|
|Avez des services de niveau intermédiaire qui doivent se connecter à SQL Database ou SQL Data Warehouse|Utilisez l’[authentification intégrée Azure AD](sql-database-aad-authentication-configure.md).|
|||

### <a name="how-do-i-limit-or-control-connectivity-access-to-my-database"></a>Comment faire pour limiter ou contrôler l’accès à la connexion à ma base de données ?
Il existe plusieurs techniques à votre disposition pour garantir une organisation de connectivité optimale à votre application. 
- Règles de pare-feu
- Points de terminaison de service de réseau virtuel
- IP réservées

#### <a name="firewall"></a>Pare-feu
Un pare-feu empêche l’accès à votre serveur à partir d’une entité externe en autorisant uniquement l’accès à votre serveur logique à des entités spécifiques. Par défaut, toutes les connexions et bases de données sont refusées au sein du serveur logique, à l’exception des connexions provenant d’autres services Azure. Avec une règle de pare-feu, vous pouvez ouvrir l’accès à votre serveur à certaines entités uniquement (par exemple, un ordinateur de développeur) que vous approuvez, en autorisant l’adresse IP correspondante à traverser le pare-feu. Une règle vous permet également de spécifier une plage d’adresses IP auxquelles vous autorisez l’accès au serveur logique. Par exemple, vous pouvez rapidement ajouter toutes les adresses IP des ordinateurs de développeur de votre organisation en spécifiant une plage dans la page des paramètres du pare-feu. 

Vous pouvez créer des règles de pare-feu au niveau du serveur ou de la base de données. Pour créer des règles de pare-feu au niveau du serveur, vous pouvez utiliser soit le portail, soit SSMS. Pour en savoir plus sur la façon de définir une règle de pare-feu au niveau du serveur et de la base de données, consultez : [Créer des règles de pare-feu dans SQL Database](sql-database-security-tutorial.md#create-a-server-level-firewall-rule-in-the-azure-portal).

#### <a name="service-endpoints"></a>Points de terminaison de service
Par défaut, votre service SQL Database est configuré pour « Autoriser tous les services Azure », ce qui signifie que toutes les machines virtuelles dans Azure peuvent essayer de se connecter à votre base de données. Ces tentatives doivent quand même faire l’objet d’une authentification. Néanmoins, si vous ne voulez pas que votre base de données soit accessible par toutes les adresses IP Azure, vous pouvez désactiver « Autoriser tous les services Azure ». De plus, vous pouvez configurer des [points de terminaison de service de réseau virtuel](sql-database-vnet-service-endpoint-rule-overview.md).

Les points de terminaison de service vous permettent d’exposer vos ressources Azure critiques uniquement à votre propre réseau privé virtuel dans Azure. Ainsi, vous éliminez simplement tout accès public à vos ressources. Le trafic entre votre réseau virtuel et Azure reste sur le réseau principal Azure. Sans point de terminaison de service, vous obtenez un routage de paquets par tunneling forcé. Votre réseau virtuel force le trafic Internet vers votre organisation et le trafic du service Azure à emprunter le même itinéraire. Avec des points de terminaison de service, vous pouvez optimiser ce trafic puisque les paquets transitent directement depuis votre réseau virtuel vers le service sur le réseau principal Azure.

![Points de terminaison de service de réseau virtuel](./media/sql-database-manage-after-migration/vnet-service-endpoints.png) 

#### <a name="reserved-ips"></a>IP réservées
Vous pouvez également provisionner des [adresses IP réservées](../virtual-network/virtual-networks-reserved-public-ip.md) pour vos machines virtuelles, et mettre en liste verte ces adresses IP de machines virtuelles spécifiques dans les paramètres de pare-feu du serveur. En affectant des adresses IP réservées, vous évitez de devoir mettre à jour les règles du pare-feu en cas de changement des adresses IP.

### <a name="what-port-do-i-connect-to-sql-database-on"></a>Sur quel port dois-je me connecter à SQL Database ?

Port 1433. SQL Database communique par le biais de ce port. Pour vous connecter à partir d’un réseau d’entreprise, vous devez ajouter une règle de trafic sortant dans les paramètres du pare-feu de votre organisation. En règle générale, évitez d’exposer le port 1433 hors de la limite Azure. Vous pouvez exécuter SSMS dans Azure via [Azure RemoteApp](https://www.microsoft.com/cloud-platform/azure-remoteapp-client-apps). Cela vous dispense d’ouvrir des connexions sortantes pour le port 1433. Comme l’adresse IP est statique, la base de données peut être ouverte uniquement pour RemoteApp. MFA (Multi-Factor Authentication) est pris en charge.

### <a name="how-can-i-monitor-and-regulate-activity-on-my-server-and-database-in-sql-database"></a>Comment puis-je surveiller et réguler l’activité sur mon serveur et ma base de données dans SQL Database ?
#### <a name="sql-database-auditing"></a>Audit SQL Database
Avec SQL Database, vous pouvez activer l’audit pour suivre les événements de la base de données. [L’audit SQL Database](sql-database-auditing.md) enregistre les événements de base de données et les écrit dans un fichier journal d’audit de votre compte de stockage Azure. L’audit s’avère particulièrement utile si vous voulez obtenir un aperçu des violations potentielles de la sécurité et des stratégies, assurer une mise en conformité avec les réglementations applicables, etc. Il vous permet de définir et configurer certaines catégories d’événements à auditer. Ainsi, vous pouvez obtenir des rapports préconfigurés et un tableau de bord pour obtenir une vue d’ensemble des événements qui se produisent sur votre base de données. Vous pouvez appliquer ces stratégies d’audit au niveau de la base de données ou au niveau du serveur. Pour plus d’informations sur la façon d’activer l’audit pour votre serveur/base de données, consultez : [Activer l’audit SQL Database](sql-database-security-tutorial.md#enable-sql-database-auditing-if-necessary).

#### <a name="threat-detection"></a>Détection des menaces
Avec la [détection des menaces](sql-database-threat-detection.md), vous avez la possibilité de réagir aux violations de stratégie ou de sécurité découvertes par l’audit très facilement. Nul besoin d’être un expert en matière de sécurité pour traiter les menaces ou violations potentielles dans votre système. La détection des menaces propose également des fonctions intégrées comme la détection d’injection de code SQL. Une injection de code SQL est une tentative de modifier ou de compromettre les données et une manière très courante d’attaquer une application de base de données de façon générale. La détection des menaces de SQL Database exécute plusieurs ensembles d’algorithmes qui détectent les vulnérabilités potentielles et les attaques par injection de code SQL, ainsi que les modèles anormaux d’accès aux bases de données (par exemple, les accès à partir d’un emplacement inhabituel ou par un principal inconnu). Les responsables sécurité ou les administrateurs désignés reçoivent une notification par e-mail si une menace est détectée sur la base de données. Chaque notification fournit des détails sur l’activité suspecte, ainsi que des recommandations sur l’analyse et l’atténuation de la menace. Pour apprendre à activer la détection des menaces, consultez : [Activer la détection des menaces SQL Database](sql-database-security-tutorial.md#enable-sql-database-threat-detection). 
### <a name="how-do-i-protect-my-data-in-general-on-sql-database"></a>Comment faire pour protéger mes données de façon générale sur SQL Database ?
Le chiffrement constitue un puissant mécanisme de protection et de sécurisation de vos données sensibles contre les intrus. Vos données chiffrées ne sont d’aucune utilité à l’intrus s’il n’a pas la clé de déchiffrement. Par conséquent, le chiffrement ajoute une couche supplémentaire de protection aux couches de sécurité existantes intégrées à SQL Database. La protection de vos données dans SQL Database porte sur deux catégories de données : 
- Vos données au repos dans les fichiers journaux et de données. 
- Vos données en transit. 

Dans SQL Database, par défaut, vos données au repos dans les fichiers journaux et de données du sous-système de stockage sont entièrement et toujours chiffrées par le biais de [Transparent Data Encryption [TDE]](/sql/relational-databases/security/encryption/transparent-data-encryption-azure-sql). Vos sauvegardes sont également chiffrées. Avec TDE, aucune modification n’est exigée du côté de l’application qui accède à ces données. Le chiffrement et le déchiffrement se produisent de manière transparente, d’où le nom. Pour protéger vos données sensibles en transit et au repos, SQL Database propose une fonctionnalité appelée [Always Encrypted (AE)](/sql/relational-databases/security/encryption/always-encrypted-database-engine). AE est une forme de chiffrement côté client qui permet de chiffrer les colonnes sensibles de votre base de données (elles sont en texte chiffré pour les administrateurs de base de données et les utilisateurs non autorisés). Au départ, le serveur reçoit les données chiffrées. La clé de chiffrement Always Encrypted est également stockée côté client, pour permettre uniquement aux clients autorisés de déchiffrer les colonnes sensibles. Les administrateurs du serveur et des données ne peuvent pas voir les données sensibles, car les clés de chiffrement sont stockées sur le client. AE chiffre les colonnes sensibles de la table, de bout en bout, depuis les clients non autorisés jusqu’au disque physique. AE prend en charge les comparaisons d’égalité, ce qui permet aux administrateurs de base de données de continuer à interroger les colonnes chiffrées quand ils exécutent des commandes SQL. Vous pouvez utiliser Always Encrypted avec diverses options de magasin de clés, par exemple [Azure Key Vault](sql-database-always-encrypted-azure-key-vault.md), le magasin de certificats Windows et les modules de sécurité matériels locaux.

|**Caractéristiques**|**Always Encrypted**|**Chiffrement transparent des données**|
|---|---|---|
|**Étendue de chiffrement**|Bout en bout|Données au repos|
|**Le serveur de base de données peut accéder aux données sensibles**|Non|Oui, étant donné que le chiffrement concerne les données au repos|
|**Opérations T-SQL autorisées**|Comparaison d’égalité|Toute la surface d’exposition T-SQL est disponible|
|**Modifications de l’application exigées pour utiliser la fonctionnalité**|Minimales|Très minimes|
|**Granularité de chiffrement**|Au niveau des colonnes|Au niveau de la base de données|
||||

### <a name="how-can-i-limit-access-to-sensitive-data-in-my-database"></a>Comment puis-je limiter l’accès aux données sensibles dans ma base de données ?
Chaque application comporte des données sensibles dans la base de données qui ont besoin d’une protection afin de ne pas être visibles par tous. Certains employés de l’organisation ont besoin de consulter ces données, tandis que d’autres ne doivent pas être en mesure de les afficher. C’est le cas des salaires des employés, par exemple. Un manager a besoin d’accéder aux informations sur les salaires de ses collaborateurs directs, tandis que les membres de son équipe ne doivent pas pouvoir accéder aux informations salariales individuelles de chacun. Un autre scénario a trait aux développeurs de données amenés à manipuler des données sensibles lors des phases de développement ou de test, par exemple, les numéros de sécurité sociale de clients. Là encore, ces informations n’ont pas besoin d’être exposées aux développeurs. Dans de telles situations, vos données sensibles ont besoin d’être masquées ou carrément non exposées. SQL Database propose deux approches permettant d’empêcher les utilisateurs non autorisés d’afficher des données sensibles :

[Dynamic Data Masking](sql-database-dynamic-data-masking-get-started.md) est une fonctionnalité de masquage de données qui vous permet de limiter l’exposition des données sensibles en les masquant aux utilisateurs qui n’ont aucun privilège sur la couche Application. Vous définissez une règle de masquage qui permet de créer un modèle de masquage (par exemple, pour afficher uniquement les quatre derniers chiffres d’un numéro d’identification quelconque, utilisez un modèle de type XXX-XX-0000 qui permet de masquer le reste avec des X) et d’identifier les utilisateurs à exclure de la règle de masquage. Le masquage se produit à la volée et il existe diverses fonctions de masquage disponibles pour diverses catégories de données. Le masquage dynamique des données vous permet de détecter automatiquement les données sensibles dans votre base de données et de leur appliquer des masques.

La fonctionnalité [Sécurité au niveau des lignes](/sql/relational-databases/security/row-level-security) vous permet de contrôler l’accès au niveau des lignes. Cela signifie que certaines lignes d’une table de base de données sont masquées en fonction de l’utilisateur qui exécute la requête (par exemple, en fonction de son appartenance à un groupe ou d’un contexte d’exécution). La restriction d’accès s’effectue sur la couche Base de données au lieu de la couche Application, ce qui simplifie votre logique d’application. Vous commencez par créer un prédicat de filtre, lequel permet de filtrer les lignes à ne pas exposer, puis vous créez la stratégie de sécurité pour définir qui a accès à ces lignes. Enfin, l’utilisateur final exécute sa requête et, en fonction de ses privilèges, il peut afficher ces lignes à accès restreint ou il ne les voit pas du tout.

### <a name="how-do-i-manage-encryption-keys-in-the-cloud"></a>Comment faire pour gérer les clés de chiffrement dans le cloud ?

Il existe des options relatives à la gestion des clés pour Always Encrypted (chiffrement côté client) et Transparent Data Encryption (chiffrement au repos). Il est recommandé de faire tourner régulièrement les clés de chiffrement. La fréquence de rotation doit respecter à la fois la réglementation et les exigences de conformité de votre organisation interne.

**TDE (Transparent Data Encryption)** : il existe une hiérarchie à deux clés dans TDE. Les données de chaque base de données utilisateur sont chiffrées par une clé de chiffrement de base de données AES-256 symétrique (spécifique à la base de données), qui est à son tour chiffrée par une clé principale RSA 2048 asymétrique (spécifique au serveur). La clé principale peut être gérée de plusieurs façons :
- Automatiquement par la plateforme : SQL Database.
- En utilisant [Azure Key Vault](sql-database-always-encrypted-azure-key-vault.md) comme magasin de clés.

Par défaut, la clé principale liée à Transparent Data Encryption est gérée par le service SQL Database pour des raisons pratiques. Si votre organisation souhaite contrôler la clé principale, il est possible d’utiliser Azure Key Vault](sql-database-always-encrypted-azure-key-vault.md) comme magasin de clés. Avec Azure Key Vault, votre organisation contrôle le provisionnement, la rotation et les autorisations spécifiques aux clés. [La rotation ou le changement de type d’une clé principale TDE](/sql/relational-databases/security/encryption/transparent-data-encryption-byok-azure-sql-key-rotation) demande peu de temps, car il suffit de rechiffrer la clé de chiffrement de base de données. Dans les organisations qui appliquent une séparation des rôles entre la gestion de la sécurité et celle des données, l’administrateur de la sécurité peut provisionner le matériel de clé pour la clé principale TDE dans Azure Key Vault, et fournir à l’administrateur de base de données un identificateur de clé Azure Key Vault pour le chiffrement au repos sur un serveur. Key Vault a été conçu de façon que Microsoft ne puisse pas voir ni extraire des clés de chiffrement. Vous bénéficiez également d’une gestion centralisée des clés pour votre organisation. 

**Always Encrypted** : il existe aussi une [hiérarchie à deux clés](/sql/relational-databases/security/encryption/overview-of-key-management-for-always-encrypted) dans Always Encrypted. Une colonne de données sensibles est chiffrée par une clé de chiffrement de colonne AES 256, qui est à son tour chiffrée par une clé principale de colonne. Les pilotes clients fournis pour Always Encrypted n’ont pas de limites concernant la longueur des clés principales de colonne. La valeur chiffrée de la clé de chiffrement de colonne est stockée dans la base de données, et la clé principale de colonne est stockée dans un magasin de clés approuvé, par exemple le magasin de certificats Windows, Azure Key Vault ou un module de sécurité matériel. 
- Vous pouvez changer [la clé de chiffrement de colonne et la clé principale de colonne](/sql/relational-databases/security/encryption/rotate-always-encrypted-keys-using-powershell). 
- La rotation de la clé de chiffrement de colonne est une opération qui dépend de la taille des données ; elle peut prendre beaucoup de temps selon la taille des tables qui contiennent les colonnes chiffrées. Ainsi, il est préférable de planifier les rotations de clés de chiffrement de colonne en conséquence. 
- La rotation des clés principales de colonne, quant à elle, n’interfère pas avec les performances des bases de données. Vous pouvez l’effectuer avec des rôles distincts.
Le diagramme suivant montre les options relatives au magasin de clés pour les clés principales de colonne dans Always Encrypted

![Fournisseurs de magasins de clés principales de colonne Always Encrypted](./media/sql-database-manage-after-migration/always-encrypted.png)

### <a name="how-can-i-optimize-and-secure-the-traffic-between-my-organization-and-sql-database"></a>Comment puis-je optimiser et sécuriser le trafic entre mon organisation et SQL Database ?
Le trafic réseau entre votre organisation et SQL Database est généralement acheminé par le biais du réseau public. Toutefois, si vous choisissez d’optimiser ce parcours et de le rendre plus sécurisé, vous pouvez envisager d’utiliser Express Route. Express Route vous permet avant tout d’étendre votre réseau d’entreprise dans la plateforme Azure par le biais d’une connexion privée. Ainsi, vous ne passez pas par l’Internet public. Vous obtenez également une sécurité, une fiabilité et une optimisation du routage accrues qui se traduisent par des latences réseau inférieures et des débits beaucoup plus rapides que ceux que vous expérimenteriez par le bais de l’Internet public en temps normal. Si vous envisagez de transférer un bloc important de données entre votre organisation et Azure, l’utilisation d’Express Route peut permettre de réduire vos coûts. Vous avez trois modèles de connectivité différents à votre disposition pour la connexion entre votre organisation et Azure : 
- [Colocalisation avec échange de cloud](../expressroute/expressroute-connectivity-models.md#CloudExchange)
- [Connexion universelle](../expressroute/expressroute-connectivity-models.md#IPVPN)
- [Connexion point à point](../expressroute/expressroute-connectivity-models.md#Ethernet)

Express Route vous permet également de doubler la limite de bande passante que vous achetez sans frais supplémentaires. Vous pouvez également configurer une connectivité interrégion à l’aide d’ExpressRoute. Pour obtenir la liste des fournisseurs de connectivité ER, consultez : [Partenaires et emplacements d’homologation Express Route](../expressroute/expressroute-locations.md). Les articles suivants décrivent Express Route de façon plus approfondie :
- [Présentation d’ExpressRoute](../expressroute/expressroute-introduction.md)
- [Configuration requise](../expressroute/expressroute-prerequisites.md)
- [Flux de travail](../expressroute/expressroute-workflows.md)

### <a name="is-sql-database-compliant-with-any-regulatory-requirements-and-how-does-that-help-with-my-own-organizations-compliance"></a>Est-ce que SQL Database est conforme aux exigences réglementaires et comment cela peut-il répondre aux exigences de conformité de mon organisation ?
SQL Database est conforme à un certain nombre d’exigences réglementaires. Pour voir quels sont les derniers points de conformité respectés, visitez [Microsoft Trust Center](https://www.microsoft.com/trustcenter/compliance/complianceofferings) et recherchez les points de conformité importants pour votre organisation. Ainsi, vous pourrez déterminer si SQL Database fait partie des services Azure conformes. Il est important de noter que même si SQL Database peut être certifié en tant que service conforme, il contribue à la conformité du service de votre organisation sans représenter pour autant une garantie automatique.

## <a name="intelligent-database-monitoring-and-maintenance-after-migration"></a>Surveillance et maintenance de bases de données intelligentes après la migration

Une fois que vous avez effectué la migration de votre base de données vers SQL Database, vous avez besoin de surveiller votre base de données (par exemple, vérifier l’utilisation des ressources ou effectuer des vérifications DBCC) et d’effectuer une maintenance régulière (par exemple, regénérer ou réorganiser les index, les statistiques, etc.). Heureusement, SQL Database est intelligent dans le sens où il utilise les tendances historiques et les métriques et statistiques enregistrées pour vous aider à surveiller et gérer de manière proactive votre base de données, afin que votre application s’exécute toujours de façon optimale. Dans certains cas, Azure SQL Database peut effectuer automatiquement des tâches de maintenance en fonction de vos paramètres de configuration. La surveillance de votre base de données revêt trois facettes dans SQL Database :
- Surveillance et optimisation des performances.
- Optimisation de la sécurité.
- Optimisation des coûts.

**Surveillance et optimisation des performances** : avec Query Performance Insight, vous pouvez obtenir des recommandations sur mesure pour votre charge de travail de base de données afin que vos applications puissent continuer à s’exécuter à un niveau optimal, de façon permanente. Vous pouvez également le configurer de sorte que ces recommandations s’appliquent automatiquement et que vous n’ayez pas à vous soucier d’effectuer d’autres tâches de maintenance. Avec Index Advisor, vous pouvez implémenter automatiquement des recommandations d’index en fonction de votre charge de travail : il s’agit d’un paramétrage automatique. Les recommandations évoluent au même rythme que la charge de travail de votre application pour fournir des suggestions pertinentes. Vous avez également la possibilité de passer manuellement en revue ces recommandations et de les appliquer à votre convenance.  

**Optimisation de la sécurité** : SQL Database fournit des recommandations actionnables en matière de sécurité pour vous aider à sécuriser vos données. De plus, la détection des menaces permet d’identifier et d’étudier les activités de base de données suspectes risquant de poser problème pour la base de données. L’[évaluation des vulnérabilités SQL](sql-vulnerability-assessment.md) est un service d’analyse et de rapport de base de données qui vous permet de surveiller l’état de sécurité de vos bases de données à grande échelle, et d’identifier les risques de sécurité et les dérives par rapport à la base de référence que vous avez définie pour la sécurité. Après chaque analyse, une liste personnalisée d’étapes à entreprendre et des scripts de correction sont proposés, ainsi qu’un rapport d’évaluation qui peut vous aider à répondre aux exigences de conformité.

Avec Azure Security Center, vous identifiez les recommandations en matière de sécurité dans le tableau de bord et vous les appliquez en un seul clic. 

**Optimisation des coûts** : la plateforme Azure SQL analyse l’historique de l’utilisation de toutes les bases de données d’un serveur pour évaluer et vous recommander des options d’optimisation des coûts. Cette analyse prend généralement une quinzaine de jours pour générer des recommandations actionnables. Le pool élastique est l’une de ces options. La recommandation apparaît dans le portail sous forme de bannière :

![recommandations de pool élastique](./media/sql-database-manage-after-migration/elastic-pool-recommendations.png) 

Vous pouvez également afficher cette analyse sous la section « Advisor » :

![recommandations de pool élastique - Advisor](./media/sql-database-manage-after-migration/advisor-section.png)

### <a name="how-do-i-monitor-the-performance-and-resource-utilization-in-sql-database"></a>Comment faire pour surveiller les performances et l’utilisation des ressources dans SQL Database ?

Dans SQL Database, vous pouvez exploiter les analyses intelligentes de la plateforme pour surveiller les performances et les ajuster en conséquence. Vous pouvez surveiller les performances et l’utilisation des ressources dans SQL Database à l’aide des méthodes suivantes :
- **Portail Azure** : le portail Azure montre l’utilisation d’une base de données unique quand vous la sélectionnez et que vous cliquez sur le graphique du volet Vue d’ensemble. Vous pouvez modifier le graphique pour afficher plusieurs métriques, notamment le pourcentage d’UC, le pourcentage de DTU, le pourcentage d’E/S de données, le pourcentage de sessions et le pourcentage de taille de base de données.

   ![Graphique de surveillance](./media/sql-database-manage-after-migration/monitoring-chart.png)

   ![Graphique de surveillance2](./media/sql-database-manage-after-migration/chart.png)

À partir de ce graphique, vous pouvez également configurer des alertes par ressource. Ces alertes vous permettent de réagir à certaines situations spécifiques aux ressources par l’envoi d’un e-mail, d’écrire sur un point de terminaison HTTPS/HTTP ou d’effectuer une action. Consultez [Surveillance des performances d’une base de données dans SQL Database](sql-database-single-database-monitor.md) pour obtenir des instructions détaillées.

- **Vues de gestion dynamique** : vous pouvez interroger la vue de gestion dynamique [sys.dm_db_resource_stats](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database) pour retourner l’historique des statistiques de consommation des ressources de la dernière heure, et la vue de catalogue système [sys.resource_stats](/sql/relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database) pour retourner l’historique des 14 derniers jours.
- **Query Performance Insight** : [Query Performance Insight](sql-database-query-performance.md) vous permet de voir l’historique des requêtes les plus consommatrices de ressources et des requêtes les plus longues pour une base de données spécifique. Vous pouvez rapidement identifier les requêtes principales par utilisation des ressources, durée et fréquence d’exécution. Vous pouvez effectuer le suivi des requêtes et détecter une régression. Cette fonctionnalité nécessite l’activation du [Magasin des requêtes](/sql/relational-databases/performance/monitoring-performance-by-using-the-query-store) pour la base de données.

   ![Query Performance Insight](./media/sql-database-manage-after-migration/query-performance-insight.png)

- **Azure SQL Analytics (préversion) dans Log Analytics** : [Azure Log Analytics](../log-analytics/log-analytics-azure-sql.md) vous permet de collecter et de visualiser les métriques de performance clés SQL Azure. Il peut prendre en charge jusqu’à 150 000 bases de données SQL Database et 5 000 pools élastiques SQL par espace de travail. Vous pouvez l’utiliser à des fins de surveillance et pour recevoir des notifications. Vous pouvez surveiller les métriques de SQL Database et des pools élastiques de plusieurs abonnements Azure. De plus, vous pouvez utiliser les pools élastiques pour identifier les problèmes à chaque couche d’une pile d’applications.

### <a name="i-am-noticing-performance-issues-how-does-my-sql-database-troubleshooting-methodology-differ-from-sql-server"></a>Je remarque des problèmes de performance : en quoi ma méthodologie de résolution des problèmes dans SQL Database diffère-t-elle de celle de SQL Server ?
La majorité des techniques de résolution de problèmes que vous utiliseriez pour diagnostiquer des problèmes de performance des requêtes et des bases de données restent les mêmes. Après tout, c’est le même moteur SQL Server qui alimente le cloud. Toutefois, la plateforme Azure SQL Database est dotée d’une « intelligence » intégrée. Celle-ci peut vous aider à résoudre et détecter les problèmes de performance encore plus facilement. Elle peut également effectuer certaines actions correctives à votre place et dans certains cas, résoudre les problèmes automatiquement de façon proactive. 

Votre approche de la résolution des problèmes de performance peut considérablement tirer parti des fonctionnalités intelligentes comme [Query Performance Insight (QPI)](sql-database-query-performance.md) et [Database Advisor](sql-database-advisor.md) utilisées conjointement ; c’est là que la méthodologie diffère car vous n’avez plus besoin d’examiner manuellement les détails essentiels pouvant vous aider à résoudre le problème. La plateforme fait le travail difficile à votre place. La fonctionnalité QPI en est l’exemple. En effet, elle vous permet d’explorer jusqu’au niveau de la requête et d’examiner les tendances historiques pour déterminer à quel moment précis la requête a régressé. Database Advisor vous fournit des recommandations visant à améliorer les performances globales, par exemple, sur les index manquants, les suppressions d’index, le paramétrage de vos requêtes, etc. 

Avec la résolution des problèmes de performance, il est important de déterminer si c’est uniquement l’application ou aussi la base de données qui l’accompagne, qui affectent les performances de votre application. Le problème de performance se trouve souvent dans la couche Application. Il peut être lié à l’architecture ou au modèle d’accès aux données. Supposez, par exemple, que vous avez une application bavarde sensible à la latence du réseau. Ainsi, votre application souffre, car de nombreuses requêtes courtes vont et viennent (dues à ce bavardage intense) entre l’application et le serveur et, sur un réseau encombré, ces allers-retours s’accumulent rapidement. Pour améliorer les performances dans cet exemple, vous pouvez utiliser un [traitement par lot des requêtes](sql-database-performance-guidance.md#batch-queries). L’utilisation de lots vous aide considérablement, car vos requêtes sont alors traitées dans un lot ; ainsi, vous réduisez la latence des allers-retours et vous améliorez les performances de votre application. 

De plus, si vous constatez une détérioration des performances globales de votre base de données, vous pouvez surveiller les vues de gestion dynamique [sys.dm_db_resource_stats](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database) et [sys.resource_stats](/sql/relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database) pour comprendre comment sont consommées l’UC, les E/S (entrées/sorties) et la mémoire. Vos performances sont peut-être affectées parce que votre base de données est sous-alimentée en ressources. Vous devez peut-être changer le niveau de performance et/ou le niveau de service en fonction des demandes de charge de travail croissantes et décroissantes. 

Pour obtenir un ensemble complet de recommandations sur les problèmes d’optimisation du niveau de performance, consultez : [Optimiser votre base de données](sql-database-performance-guidance.md#tune-your-database).

### <a name="how-do-i-ensure-i-am-using-the-appropriate-service-tier-and-performance-level"></a>Comment vérifier si j’utilise les niveaux de performance et de service appropriés ?
SQL Database propose plusieurs niveaux de service : De base, Standard et Premium. Chaque niveau de service vous permet d’obtenir les performances prévisibles garanties liées à ce niveau de service. En fonction de votre charge de travail, vous pouvez avoir des pics d’activité qui font atteindre à l’utilisation de vos ressources le plafond de votre niveau de performance actuel. Le cas échéant, commencez judicieusement par déterminer si un paramétrage peut résoudre le problème (par exemple, en ajoutant ou en modifiant un index, etc.). Si vous rencontrez toujours des problèmes de limite, envisagez de passer à un niveau de performance ou de service supérieur. 

|**Niveau de service**|**Scénarios de cas d’usage courants**|
|---|---|
|**De base**|Applications avec une poignée d’utilisateurs et une base de données sans besoins de concurrence, de mise à l’échelle et de performances élevés. |
|**Standard**|Applications qui ont des besoins de concurrence, de mise à l’échelle et de performances considérables associés à des demandes d’E/S faibles à moyennes. |
|**Premium**|Applications avec un grand nombre d’utilisateurs simultanés, des besoins d’UC/mémoire élevés et des demandes d’E/S élevées. Les applications à concurrence élevée, à débit élevé et sensibles à la latence peuvent exploiter le niveau Premium. |
|||

Pour vérifier la pertinence de votre niveau de performance, vous pouvez surveiller votre consommation des ressources de requête et de base de données de l’une des manières mentionnées ci-dessus dans « Comment faire pour surveiller les performances et l’utilisation des ressources dans SQL Database ? ». Si vous trouvez que vos requêtes/bases de données flirtent constamment avec les limites d’UC/mémoire, envisagez de passer à un niveau de performance supérieur. De même, si vous remarquez que, même pendant vos heures de pointe, vous n’utilisez pas tant que ça les ressources, envisagez de passer à un niveau de performance inférieur à votre niveau actuel. 

Si vous utilisez un modèle d’application SaaS ou un scénario de consolidation de bases de données, envisagez d’utiliser un pool élastique pour optimiser les coûts. Un pool élastique est un excellent moyen pour consolider des bases de données et optimiser les coûts. Pour en savoir plus sur la gestion de plusieurs bases de données à l’aide d’un pool élastique, consultez : [Gérer des pools et des bases de données](sql-database-elastic-pool.md#manage-elastic-pools-and-databases-using-the-azure-portal). 

### <a name="how-often-do-i-need-to-run-database-integrity-checks-for-my-database"></a>À quelle fréquence ai-je besoin d’exécuter les vérifications de l’intégrité de ma base de données ?
SQL Database utilise des techniques intelligentes pour gérer certaines classes d’altération des données automatiquement et sans perte de données. Ces techniques sont intégrées au service et exploitées par lui au moment opportun. Régulièrement, vos sauvegardes de base de données sont testées sur le service en effectuant leur restauration et en exécutant DBCC CHECKDB. SQL Database traite les problèmes de façon proactive le cas échéant. La [réparation de page automatique](/sql/sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring) est exploitée pour corriger les pages endommagées ou présentant des problèmes d’intégrité des données. Les pages de base de données sont toujours vérifiées avec le paramètre CHECKSUM par défaut qui vérifie l’intégrité de la page. SQL Database surveille et examine l’intégrité des données de votre base de données de manière proactive et, si des problèmes surgissent, les traite avec la priorité la plus élevée. De plus, vous pouvez éventuellement choisir d’exécuter vos propres vérifications d’intégrité à votre convenance.  Pour plus d’informations, consultez [Intégrité des données dans SQL Database](https://azure.microsoft.com/blog/data-integrity-in-azure-sql-database/).

## <a name="data-movement-after-migration"></a>Mouvement des données après la migration

### <a name="how-do-i-export-and-import-data-as-bacpac-files-from-sql-database"></a>Comment faire pour exporter et importer des données en tant que fichiers BACPAC à partir de SQL Database ?

- **Export** : vous pouvez exporter votre base de données Azure SQL Database en tant que fichier BACPAC à partir du portail Azure.

   ![exportation de base de données](./media/sql-database-export/database-export.png)

- **Import** : vous pouvez également importer des données sous forme de fichier BACPAC dans la base de données à l’aide du portail Azure.

   ![importation de base de données](./media/sql-database-import/import.png)

### <a name="how-do-i-synchronize-data-between-sql-database-and-sql-server"></a>Comment faire pour synchroniser des données entre SQL Database et SQL Server ?
Il existe plusieurs méthodes : 
- La fonctionnalité **[Data Sync](sql-database-sync-data.md)** vous permet de synchroniser les données de façon bidirectionnelle entre plusieurs bases de données SQL Server locales et SQL Database. Pour synchroniser des bases de données SQL Server locales, vous devez installer et configurer l’agent de synchronisation sur un ordinateur local et ouvrir le port TCP sortant 1433.
- La fonctionnalité **[Réplication transactionnelle](https://azure.microsoft.com/en-us/blog/transactional-replication-to-azure-sql-database-is-now-generally-available/)** vous permet de synchroniser vos données locales avec Azure SQL Azure, le serveur de publication étant la base de données locale et l’abonné étant Azure SQL Database. Pour l’instant, seule cette configuration est prise en charge. Pour plus d’informations sur la façon de faire migrer vos données locales vers Azure SQL Database avec un temps d’arrêt minimal, consultez : [Utiliser la réplication transactionnelle](sql-database-cloud-migrate.md#method-2-use-transactional-replication).

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur [SQL Database](sql-database-technical-overview.md).

