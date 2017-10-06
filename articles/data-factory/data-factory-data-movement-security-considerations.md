---
title: "Considérations relatives à l’aaaSecurity pour le déplacement des données dans Azure Data Factory | Documents Microsoft"
description: "Découvrez comment sécuriser les déplacements de données dans Azure Data Factory."
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 4bfce8884df14ad5b94e28ad3dfcf7025e2130a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---security-considerations-for-data-movement"></a>Azure Data Factory - Considérations de sécurité relatives au déplacement des données
## <a name="introduction"></a>Introduction
Cet article décrit l’infrastructure de sécurité de base que les services de déplacement des données dans Azure Data Factory utiliser toosecure vos données. Les ressources de gestion d’Azure Data Factory reposent sur l’infrastructure de sécurité Azure et utilisent toutes les mesures de sécurité proposées par Azure.

Dans une solution Data Factory, vous créez un ou plusieurs [pipelines](data-factory-create-pipelines.md) de données. Un pipeline constitue un regroupement logique d’activités qui exécutent ensemble une tâche. Ces pipelines résident dans la région de hello où la fabrique de données hello a été créé. 

Bien que la fabrique de données est uniquement disponible dans **ouest des États-Unis**, **États-Unis**, et **Europe du Nord** régions, le service de déplacement des données hello est disponible [globalement dans plusieurs régions](data-factory-data-movement-activities.md#global). Fabrique de données service garantit que les données ne laissent pas une zone géographique / région, sauf si vous le demander explicitement hello service toouse une autre région si le service de déplacement de données hello n’est pas encore déployé toothat région. 

Azure Data Factory ne stocke aucune donnée à l’exception des informations d’identification du service lié pour les banques de données cloud, qui sont chiffrées à l’aide de certificats. Vous permet de créer des flux de travail pilotés par les données tooorchestrate les mouvements de données entre [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats) et le traitement des données à l’aide [les services de calcul](data-factory-compute-linked-services.md) dans d’autres régions ou dans un site local environnement. Il vous permet également de trop[surveiller et gérer des flux de travail](data-factory-monitor-manage-pipelines.md) à la fois par programme et les mécanismes de l’interface utilisateur.

Le déplacement des données à l’aide d’Azure Data Factory a obtenu les **certifications** suivantes :
-   [HIPAA/HITECH](https://www.microsoft.com/en-us/trustcenter/Compliance/HIPAA)  
-   [ISO/IEC 27001](https://www.microsoft.com/en-us/trustcenter/Compliance/ISO-IEC-27001)  
-   [ISO/IEC 27018](https://www.microsoft.com/en-us/trustcenter/Compliance/ISO-IEC-27018) 
-   [CSA STAR](https://www.microsoft.com/en-us/trustcenter/Compliance/CSA-STAR-Certification)
     
Si vous êtes intéressé par la conformité Azure et comment Azure protège sa propre infrastructure, visitez hello [Microsoft Trust Center](https://www.microsoft.com/TrustCenter/default.aspx). 

Dans cet article, nous allons examiner les considérations de sécurité dans hello suivant deux scénarios de déplacement des données : 

- **Scénario cloud** : dans ce scénario, votre source et votre destination sont toutes deux accessibles publiquement via Internet. Cela inclut les services de stockage cloud gérés comme le stockage Azure, Azure SQL Data Warehouse, Azure SQL Database, Azure Data Lake Store, Amazon S3, Amazon Redshift, les services SaaS tels que Salesforce et les protocoles web tels que FTP et OData. Vous trouverez [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) une liste complète des sources de données prises en charge.
- **Scénario hybride**: dans ce scénario, votre source ou destination est derrière un pare-feu ou à l’intérieur d’une données hello ou de réseau d’entreprise sur site, le magasin est dans un réseau privé / virtuel réseau (source de hello plus souvent) et n’est pas accessible . Les serveurs de base de données hébergés sur des machines virtuelles sont également inclus dans ce scénario.

## <a name="cloud-scenarios"></a>Scénarios cloud
###<a name="securing-data-store-credentials"></a>Sécurisation des informations d’identification des banques de données
Azure Data Factory protège les informations d’identification de vos banques de données en les **chiffrant** à l’aide de **certificats gérés par Microsoft**. Ces certificats sont remplacés tous les **deux ans** (avec renouvellement des certificats et migration des informations d’identification). Ces informations d’identification chiffrées sont stockées de manière sécurisée dans un **stockage Azure géré par les services de gestion d’Azure Data Factory**. Pour plus d’informations sur la sécurité du stockage Azure, consultez l’article [Vue d’ensemble des fonctionnalités de sécurité du stockage Azure](../security/security-storage-overview.md).

### <a name="data-encryption-in-transit"></a>Chiffrement des données en transit
Si le magasin de données cloud hello prend en charge HTTPS ni TLS, toutes les données de transferts entre les services de déplacement de données dans la fabrique de données et un magasin de données cloud sont via un canal sécurisé, HTTPS ou TLS.

> [!NOTE]
> Toutes les connexions trop**base de données SQL Azure** et **Azure SQL Data Warehouse** nécessitent toujours de chiffrement (SSL/TLS) tandis que les données se trouvent dans tooand de transit à partir de la base de données hello. Lors de la création d’un pipeline à l’aide d’un éditeur JSON, ajouter hello **chiffrement** propriété et la définir trop**true** Bonjour **chaîne de connexion**. Lorsque vous utilisez hello [Assistant copie de](data-factory-azure-copy-wizard.md), Assistant de hello définit cette propriété par défaut. Pour **Azure Storage**, vous pouvez utiliser **HTTPS** dans la chaîne de connexion hello.

### <a name="data-encryption-at-rest"></a>Chiffrement des données au repos
Certaines banques de données prennent en charge le chiffrement des données au repos. Nous vous suggérons d’activer le mécanisme de chiffrement des données pour ces banques de données. 

#### <a name="azure-sql-data-warehouse"></a>Azure SQL Data Warehouse
Transparent Data Encryption (TDE) dans l’entrepôt de données SQL Azure permet à la protection contre les menaces hello d’activités malveillantes en effectuant le chiffrement en temps réel et déchiffrement de vos données au repos. Ce comportement est transparent toohello client. Pour plus d’informations, consultez [Sécuriser une base de données dans SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md).

#### <a name="azure-sql-database"></a>Base de données SQL Azure
Base de données SQL Azure prend également en charge le chiffrement transparent des données (TDE), ce qui vous permet de protéger contre les menaces hello d’activités malveillantes en effectuant le chiffrement en temps réel et le déchiffrement des données de salutation sans nécessiter de modifications toohello application. Ce comportement est transparent toohello client. Pour plus d’informations, consultez [Transparent Data Encryption avec Azure SQL Database](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database). 

#### <a name="azure-data-lake-store"></a>Azure Data Lake Store
Magasin d’Azure Data Lake fournit également le chiffrement des données stockées dans le compte de hello. Lorsque activé, le magasin de LAC de données chiffre les données avant de rendre persistantes automatiquement et déchiffre avant la récupération, rendant client toohello transparent l’accès aux données de hello. Pour plus d’informations, consultez [Sécurité dans Azure Data Lake Store](../data-lake-store/data-lake-store-security-overview.md). 

#### <a name="azure-blob-storage-and-azure-table-storage"></a>Stockage Blob Azure et Stockage de tables Azure
Stockage de Table Azure et de stockage d’objets Blob Azure prend en charge le stockage Service de chiffrement (SSE), qui chiffre automatiquement vos données avant la persistance toostorage et déchiffre avant la récupération. Pour plus d’informations, consultez [Azure Storage Service Encryption pour les données au repos](../storage/common/storage-service-encryption.md).

#### <a name="amazon-s3"></a>Amazon S3
Amazon S3 prend en charge le chiffrement des données au repos côté client et côté serveur. Pour plus d’informations, consultez [Protection des données à l’aide du chiffrement](http://docs.aws.amazon.com/AmazonS3/latest/dev/UsingEncryption.html). Actuellement, Data Factory ne prend pas en charge Amazon S3 dans un cloud privé virtuel (VPC).

#### <a name="amazon-redshift"></a>Amazon Redshift
Amazon Redshift prend en charge le chiffrement du cluster pour les données au repos. Pour plus d’informations, consultez [Amazon Redshift Database Encryption (Chiffrement de base de données Amazon Redshift)](http://docs.aws.amazon.com/redshift/latest/mgmt/working-with-db-encryption.html). Actuellement, Data Factory ne prend pas en charge Amazon Redshift dans un cloud privé virtuel (VPC). 

#### <a name="salesforce"></a>Salesforce
Salesforce prend en charge Shield Platform qui permet de chiffrer tous les fichiers, pièces jointes et champs personnalisés. Pour plus d’informations, consultez [hello présentation des flux d’authentification OAuth Web Server](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_web_server_oauth_flow.htm).  

## <a name="hybrid-scenarios-using-data-management-gateway"></a>Scénarios hybrides (à l’aide de la passerelle de gestion des données)
Scénarios hybrides nécessitent toobe passerelle de gestion des données dans un réseau local ou à l’intérieur d’un réseau virtuel (Azure) ou un cloud privé virtuel (Amazon) installé. passerelle de Hello doit être de banques de données locales en mesure de tooaccess hello. Pour plus d’informations sur la passerelle de hello, consultez [passerelle de gestion des données](data-factory-data-management-gateway.md). 

![Canaux de passerelle de gestion de données](media/data-factory-data-movement-security-considerations/data-management-gateway-channels.png)

Hello **du canal de commande** permet la communication entre les services de déplacement de données dans la fabrique de données et de la passerelle de gestion des données. communication de Hello contient des informations toohello activités associées. canal de données Hello est utilisé pour transférer des données entre les banques de données locales et les magasins de données cloud.    

### <a name="on-premises-data-store-credentials"></a>Informations d’identification des banques de données locales
informations d’identification de Hello pour vos magasins de données locale sont stockées localement (pas dans le cloud de hello). Elles peuvent être définies de trois façons différentes. 

- À l’aide de **texte brut** (moins sécurisé) via HTTPS depuis le portail Azure ou l’Assistant de copie. informations d’identification Hello sont passées dans la passerelle locale de toohello de texte brut.
- À l’aide de la **bibliothèque de chiffrement JavaScript depuis l’Assistant de copie**.
- À l’aide de **l’application Gestionnaire des informations d’identification ClickOnce**. Cliquez sur le Hello-une fois que l’application s’exécute sur l’ordinateur local, hello qui a accès toohello passerelle et définit les informations d’identification pour le magasin de données hello. Cette option et un hello sont ensuite un hello options les plus sécurisées. applications du Gestionnaire d’informations d’identification Hello, par défaut, utilise le port hello 8050 sur ordinateur hello avec la passerelle pour une communication sécurisée.  
- Utilisez [New-AzureRmDataFactoryEncryptValue](/powershell/module/azurerm.datafactories/New-AzureRmDataFactoryEncryptValue) informations d’identification de tooencrypt d’applet de commande PowerShell. applet de commande Hello utilise un certificat hello que cette passerelle est configurée toouse tooencrypt hello références. Vous pouvez utiliser des références de hello chiffré retournés par cette applet de commande et l’ajouter trop**EncryptedCredential** élément Hello **connectionString** dans le fichier JSON hello que vous utilisez avec hello [ Nouveau-AzureRmDataFactoryLinkedService](/powershell/module/azurerm.datafactories/new-azurermdatafactorylinkedservice) applet de commande ou dans l’extrait de code hello JSON Bonjour éditeur Data Factory dans le portail de hello. Cette option et hello, cliquez sur-une fois l’application sont les options les plus sécurisées hello. 

#### <a name="javascript-cryptography-library-based-encryption"></a>Chiffrement à partir de la bibliothèque de chiffrement JavaScript
Vous pouvez chiffrer les informations d’identification du magasin de données à l’aide de [bibliothèque de chiffrement de JavaScript](https://www.microsoft.com/download/details.aspx?id=52439) de hello [Assistant copie de](data-factory-copy-wizard.md). Lorsque vous sélectionnez cette option, hello Assistant copie de récupère hello de clé publique de la passerelle et qu’il utilise des informations d’identification du magasin de données tooencrypt hello. informations d’identification Hello sont déchiffrées par l’ordinateur de passerelle hello et protégées par Windows [DPAPI](https://msdn.microsoft.com/library/ms995355.aspx).

**Navigateurs pris en charge :** IE8, IE9, IE10, IE11, Microsoft Edge, ainsi que les dernières versions des navigateurs Firefox, Chrome, Opera et Safari. 

#### <a name="click-once-credentials-manager-app"></a>Application Gestionnaire des informations d’identification ClickOnce
Vous pouvez lancer hello cliquez-une fois en fonction des applications du Gestionnaire d’informations d’identification à partir de l’Assistant portail/copie Azure lors de la création de pipelines. Cette application permet de s’assurer que les informations d’identification ne sont pas transférées en texte brut acheminement hello. Par défaut, il utilise le port de hello **8050** sur l’ordinateur hello avec la passerelle pour une communication sécurisée. Ce port peut être modifié en cas de besoin.  
  
![Port HTTPS pour la passerelle de hello](media/data-factory-data-movement-security-considerations/https-port-for-gateway.png)

La passerelle de gestion des données utilise actuellement un seul **certificat**. Ce certificat est créé au cours de l’installation de la passerelle hello (s’applique tooData passerelle de gestion créée après novembre 2016 et version 2.4.xxxx.x ou version ultérieure). Vous pouvez remplacer ce certificat par votre propre certificat SSL/TLS. Ce certificat est utilisé par hello cliquez-une fois que credential manager application toosecurely Connectez l’ordinateur de passerelle toohello pour définir les informations d’identification du magasin de données. Il stocke les données les informations d’identification de magasin en toute sécurité sur site à l’aide de Windows de hello [DPAPI](https://msdn.microsoft.com/library/ms995355.aspx) sur l’ordinateur de hello avec la passerelle. 

> [!NOTE]
> Les passerelles plus anciens qui ont été installées avant novembre 2016 ou de version 2.3.xxxx.x continuent toouse d’informations d’identification chiffrées et stockées sur le cloud. Même si vous mettez à niveau de version la plus récente toohello passerelle hello, informations d’identification hello ne sont pas migrés tooan ordinateur local    
  
| Version de la passerelle (lors de la création) | Informations d’identification stockées | Chiffrement/sécurité des informations d’identification | 
| --------------------------------- | ------------------ | --------- |  
| < = 2.3.xxxx.x | Dans le cloud | Chiffré à l’aide du certificat (différent de hello celui utilisé par les applications du Gestionnaire d’informations d’identification) | 
| > = 2.4.xxxx.x | En local | Sécurisation à l’aide de DPAPI | 
  

### <a name="encryption-in-transit"></a>Chiffrement en transit
Tous les transferts de données sont via un canal sécurisé **HTTPS** et **TLS sur TCP** attaques de man-in-the-middle tooprevent pendant la communication avec les services Azure.
 
Vous pouvez également utiliser [VPN IPSec](../vpn-gateway/vpn-gateway-about-vpn-devices.md) ou [Express Route](../expressroute/expressroute-introduction.md) canal de communication sécurisé hello toofurther entre votre réseau local et le Azure.

Réseau virtuel est une représentation logique de votre réseau dans le cloud de hello. Vous pouvez vous connecter à un tooyour de réseau local sur le réseau virtuel Azure (VNet) par la configuration d’IPSec VPN (de site à site) ou Express Route (homologation privée)       

Hello tableau suivant récapitule hello réseau et passerelle de recommandations de configuration selon différentes combinaisons des emplacements source et de destination pour le déplacement de données hybrides.

| Source | Destination | Configuration réseau | Configuration de la passerelle |
| ------ | ----------- | --------------------- | ------------- | 
| Local | Machines virtuelles et services cloud déployés au sein de réseaux virtuels | VPN IPSec (de point à site ou de site à site) | La passerelle peut être installée en local ou sur une machine virtuelle Azure au sein du réseau virtuel | 
| Local | Machines virtuelles et services cloud déployés au sein de réseaux virtuels | ExpressRoute (homologation privée) | La passerelle peut être installée en local ou sur une machine virtuelle Azure au sein du réseau virtuel | 
| Local | Services Azure disposant d’un point de terminaison public | ExpressRoute (homologation publique) | La passerelle doit être installée en local | 

Hello images suivantes montrent l’utilisation de hello de passerelle de gestion des données pour le déplacement des données entre une base de données locale et les services Azure Express route et des VPN IPSec (avec un réseau virtuel) :

**Express Route :**
 
![ExpressRoute avec passerelle](media/data-factory-data-movement-security-considerations/express-route-for-gateway.png) 

**IPSec VPN :**

![VPN IPSec avec passerelle](media/data-factory-data-movement-security-considerations/ipsec-vpn-for-gateway.png)

### <a name="firewall-configurations-and-whitelisting-ip-address-of-gateway"></a>Configurations de pare-feu et autorisation des adresses IP de la passerelle

#### <a name="firewall-requirements-for-on-premisesprivate-network"></a>Configuration requise du pare-feu pour un réseau local/privé  
Dans une entreprise, un **pare-feu d’entreprise** s’exécute sur le routeur central de hello d’organisation de hello. Et, **pare-feu Windows** s’exécute comme un démon sur ordinateur local de hello sur quel hello passerelle est installée. 

Hello tableau suivant fournit des **port sortant** en matière de domaine pour hello **pare-feu d’entreprise**.

| Noms de domaine | Ports sortants | Description |
| ------------ | -------------- | ----------- | 
| `*.servicebus.windows.net` | 443, 80 | Requis par les services de déplacement hello passerelle tooconnect toodata dans la fabrique de données |
| `*.core.windows.net` | 443 | Utilisé par hello passerelle tooconnect tooAzure compte de stockage lorsque vous utilisez hello [intermédiaire copie](data-factory-copy-activity-performance.md#staged-copy) fonctionnalité. | 
| `*.frontend.clouddatahub.net` | 443 | Requis par hello passerelle tooconnect toohello service Azure Data Factory. | 
| `*.database.windows.net` | 1433   | (Facultatif) nécessaire lorsque votre destination est Azure SQL Database ou Azure SQL Data Warehouse. Hello d’utilisation mises en lots copie fonctionnalité toocopy données tooAzure SQL de base de données/Azure SQL Data Warehouse sans ouvrir le port 1433 hello. | 
| `*.azuredatalakestore.net` | 443 | (Facultatif) nécessaire lorsque votre destination est Azure Data Lake Store. | 

> [!NOTE] 
> Vous avez peut-être toomanage ports / liste approuvées des domaines à hello au niveau du pare-feu d’entreprise comme requis par les sources de données respectifs. Ce tableau utilise uniquement Azure SQL Database, Azure SQL Data Warehouse et Azure Data Lake Store comme exemples.   

Hello tableau suivant fournit des **port sortant** configuration requise pour hello **pare-feu windows**.

| Ports entrants | Description | 
| ------------- | ----------- | 
| 8050 (TCP) | Requis par hello d’informations d’identification manager application toosecurely informations d’identification définies pour les magasins de données locale sur la passerelle hello. | 

![Configuration requise des ports de la passerelle](media\data-factory-data-movement-security-considerations/gateway-port-requirements.png) 

#### <a name="ip-configurations-whitelisting-in-data-store"></a>Configuration/autorisation des adresses IP dans la banque de données
Certaines banques de données dans le cloud de hello requièrent également l’autorisation d’adresse IP de l’ordinateur hello y accéder. Vérifiez que hello adresseIP de machine de la passerelle hello dans la liste approuvée configurées dans le pare-feu de façon appropriée.

Hello banques de données de cloud suivantes requièrent autorisation d’adresse IP de l’ordinateur de passerelle hello. Certaines de ces banques de données, par défaut, peuvent nécessiter pas d’autorisation d’adresse IP de hello. 

- [Azure SQL Database](../sql-database/sql-database-firewall-configure.md) 
- [Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md#create-a-server-level-firewall-rule-in-the-azure-portal)
- [Azure Data Lake Store](../data-lake-store/data-lake-store-secure-data.md#set-ip-address-range-for-data-access)
- [Azure Cosmos DB](../documentdb/documentdb-firewall-support.md)
- [Amazon Redshift](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) 

## <a name="frequently-asked-questions"></a>Forum Aux Questions

**Question :** hello passerelle de données peut être partagée entre les fabriques de données différentes ?
**Réponse :** Nous ne prenons pas encore en charge cette fonctionnalité, mais y travaillons activement.

**Question :** quelles sont les exigences du port hello pour hello passerelle toowork ?
**Réponse :** passerelle permet les connexions HTTP tooopen internet. Hello **sortants ports 443 et 80** doit être ouvert pour la passerelle toomake cette connexion. Ouvrez **8050 de Port entrant** uniquement au niveau d’ordinateur hello (et non au niveau du pare-feu d’entreprise) pour l’application du Gestionnaire d’informations d’identification. Si la base de données SQL Azure ou Azure SQL Data Warehouse est utilisé en tant que source / destination, vous devez tooopen **1433** également le port. Pour en savoir plus, consultez la section [Configurations de pare-feu et autorisation d’adresses IP](#firewall-configurations-and-whitelisting-ip-address-of gateway). 

**Question :** Quels sont les certificats requis pour la passerelle ?
**Réponse :** passerelle actuelle requiert un certificat qui est utilisé par l’application du Gestionnaire d’informations d’identification hello pour définir en toute sécurité des informations d’identification du magasin de données. Ce certificat est un certificat auto-signé créé et configuré par le programme d’installation de la passerelle hello. Vous pouvez également utiliser votre propre certificat TLS/SSL. Pour en savoir plus, consultez la section [Application Gestionnaire des informations d’identification ClickOnce](#click-once-credentials-manager-app). 

## <a name="next-steps"></a>Étapes suivantes
Pour en savoir plus sur les performances de l’activité de copie, consultez le [Guide sur les performances et le réglage de l’activité de copie](data-factory-copy-activity-performance.md).

 
