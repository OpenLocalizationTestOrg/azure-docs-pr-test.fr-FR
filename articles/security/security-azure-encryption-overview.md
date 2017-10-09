---
title: "vue d’ensemble du chiffrement aaaAzure | Documents Microsoft"
description: "En savoir plus sur les différentes options de chiffrement dans Azure"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 08/18/2017
ms.author: barclayn
ms.openlocfilehash: ef9ab46de32b857e99e8fe628a61386b95cf197f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-overview"></a>Vue d’ensemble du chiffrement Azure

Cet article fournit une vue d’ensemble de l’utilisation du chiffrement dans Microsoft Azure Document. Elle couvre hello principales zones de chiffrement, y compris le chiffrement au repos, de chiffrement dans le vol et la gestion des clés avec le coffre de clés. Chaque section inclut des liens vers des informations plus détaillées.

## <a name="encryption-of-data-at-rest"></a>Chiffrement des données au repos

Les données au repos incluent des informations qui se trouvent dans un stockage persistant sur un support physique, sous n’importe quel format numérique. Cela inclut les fichiers sur un support magnétique ou optique, les données archivées et les sauvegardes de données. Microsoft Azure offre une variété de toomeet de solutions de stockage de données à des besoins différents, y compris les fichiers, disque, blob et stockage de table. Microsoft fournit également le chiffrement tooprotect [base de données SQL Azure](../sql-database/sql-database-technical-overview.md), [CosmosDB](../cosmos-db/introduction.md)et Azure Data Lake.

Chiffrement des données au repos n’est disponible pour les services sur hello Azure Software-as-a-Service (SaaS), Platform-as-a-Service (PaaS) et les modèles de cloud d’Infrastructure-as-a-Service (IaaS). Ce document résume et fournit des ressources toohelp vous utilisez les options de chiffrement de Azure.

Pour plus de discussion de mode de chiffrement de données au repos dans Azure, consultez le document intitulé hello [Azure Data chiffrement au repos](azure-security-encryption-atrest.md)

## <a name="azure-encryption-models"></a>Modèles de chiffrement Azure

Azure prend en charge plusieurs modèles de chiffrement, y compris le chiffrement côté serveur à l’aide de clés gérées par le service, de clés de gérées par le client dans Azure Key Vault ou à l’aide de clés gérées par le client sur du matériel de contrôlé par le client. Le chiffrement côté client vous permet de toomanage et le magasin de clés local ou dans un autre endroit sûr.

### <a name="client-side-encryption"></a>chiffrement côté client

Le chiffrement côté client est effectué en dehors d’Azure. Le chiffrement côté client inclut :

- Données chiffrées par une application qui s’exécute dans le centre de données du client hello ou par une application de service
- Les données sont déjà chiffrées lorsqu’elles sont reçues par Azure.

Avec le chiffrement côté client, fournisseur de services de cloud hello n’a pas accès aux clés de chiffrement de toohello et ne peut pas déchiffrer ces données. Vous conservez un contrôle total des clés de hello.

### <a name="server-side-encryption"></a>Chiffrement côté serveur

trois modes de chiffrement côté serveur Hello offrent les caractéristiques de gestion de clés différentes, qui peuvent être choisis selon vos besoins.

- Les **Clés gérées par le service** fournissent une combinaison de contrôle et de fonctionnalités avec une faible surcharge

- **Gérée par le client de clés** permettent de contrôler les clés hello, y compris hello capacité toobring vos propres clés (BYOK) ou le toogenerate nouveaux.

- **Géré par le service des clés dans ccustomer-controlledhardware** vous permet de clés toomanage dans votre référentiel propriétaire qui se trouve en dehors du contrôle de Microsoft. Il s’agit de l’option Héberger vos propres clés (HYOK). Toutefois, la configuration est complexe et la plupart des services Azure ne prennent pas en charge ce modèle.

### <a name="azure-disk-encryption"></a>Azure Disk Encryption

Machines virtuelles Windows et Linux peuvent être protégés à l’aide de [chiffrement de disque Azure](azure-security-disk-encryption.md), qui utilise hello [Windows BitLocker](https://technet.microsoft.com/library/cc766295(v=ws.10).aspx) technologie et Linux [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) tooprotect les disques du système d’exploitation et les disques de données avec chiffrement de volume complet.

Les clés et secrets de chiffrement sont sauvegardés dans votre abonnement [Azure Key Vault](../key-vault/key-vault-whatis.md). Vous pouvez sauvegarder et restaurer des machines virtuelles chiffrées qui sont chiffrés avec une configuration hello veillent à l’aide du service de sauvegarde Azure hello.

### <a name="azure-storage-service-encryption"></a>Chiffrement du service de stockage Azure

Les données au repos dans le stockage Azure (objet blob et fichier) peuvent être chiffrées dans les scénarios côté serveur et côté client.

[Chiffrement du Service Azure Storage](../storage/storage-service-encryption.md) (SSE) peut chiffrer automatiquement les données avant qu’il est stocké et déchiffre automatiquement lorsque vous les récupérez, rendre hello traiter complètement transparent aux utilisateurs. Chiffrement de Service de stockage utilise 256 bits [chiffrement AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), qui est un de hello les plus fortes le chiffrement par blocs disponible et gère le chiffrement, le déchiffrement et gestion des clés de manière transparente.

### <a name="client-side-encryption-of-azure-blobs"></a>Chiffrement côté client des objets blob Azure

Le chiffrement côté client d’objets blob Azure peut être effectué de différentes façons.

Vous pouvez utiliser hello bibliothèque cliente de stockage Azure pour les données de tooencrypt de package NuGet .NET au sein de votre toouploading préalable de client applications il tooAzure stockage.

toolearn plus en détail et téléchargement hello bibliothèque cliente de stockage Azure pour .NET NuGet package, consultez le document intitulé hello [8.3.0 le stockage Windows Azure](https://www.nuget.org/packages/WindowsAzure.Storage)

Lorsque vous utilisez le chiffrement côté client avec le coffre de clés Azure, vos données sont chiffrées à l’aide d’une unique symétrique contenu chiffrement clé (CEK) qui est généré par le client de stockage Azure hello SDK. Hello CEK est chiffrée à l’aide d’une clé de chiffrement (clés), qui peut être une clé symétrique ou une paire de clés asymétriques. Vous pouvez la gérer localement ou la stocker dans Azure Key Vault. Hello données chiffrées seront ensuite téléchargé de service de stockage tooAzure.

toolearn plus d’informations sur le chiffrement côté client avec Azure Key Vault et prise en main tooinstructions de procédure, consultez le document intitulé hello [didacticiel : chiffrer et déchiffrer les objets BLOB dans Microsoft Azure Storage à l’aide d’Azure Key Vault](../storage/storage-encrypt-decrypt-blobs-key-vault.md)

Enfin, vous pouvez également utiliser hello bibliothèque cliente de stockage Azure pour le chiffrement du côté client Java tooperform avant de télécharger des données tooAzure stockage et toodecrypt hello lors du téléchargement de toohello client. La bibliothèque prend également en charge l’intégration à [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) pour la gestion des clés de compte de stockage.

### <a name="encryption-of-data-at-rest-with-azure-sql-database"></a>Chiffrement des données au repos avec la base de données Azure SQL

[Azure SQL Database](../sql-database/sql-database-technical-overview.md) est une base de données relationnelle à usage général de Microsoft Azure qui prend en charge des structures telles que les données relationnelles, JSON, les données spatiales et XML. SQL Azure prend en charge le chiffrement côté serveur via la fonctionnalité de chiffrement Transparent des données (TDE) hello et chiffrement côté client via la fonctionnalité de chiffrement intégral hello.

#### <a name="transparent-data-encryption"></a>Chiffrement transparent des données

[Chiffrement TDE Transparent des données](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-tde) est utilisé tooencrypt [SQL Server](https://www.microsoft.com/sql-server/sql-server-2016), [base de données SQL Azure](../sql-database/sql-database-technical-overview.md), et [Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) en temps réel, des fichiers de données à l’aide d’une clé de chiffrement de base de données (DEK), qui est stockée dans l’enregistrement de démarrage de base de données hello pour la disponibilité lors de la récupération.

Le chiffrement transparent des données (TDE) protège les données et les fichiers journaux, à l’aide d’algorithmes de chiffrement AES et 3DES. Chiffrement du fichier de base de données hello est effectué au niveau de la page hello ; pages Hello dans une base de données sont chiffrées avant d’être écrites toodisk et sont déchiffrées quand elles sont lues en mémoire. TDE est désormais activé par défaut sur les nouvelles bases de données Azure SQL.

#### <a name="always-encrypted"></a>Always Encrypted

Hello [Always Encrypted](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-database-engine) fonctionnalité dans SQL Azure vous tooencrypt des données au sein du client applications préalable toostoring dans la base de données SQL Azure et vous permet de déléguer tooenable toothird d’administration local de base de données parties et maintenir la séparation entre ceux qui possèdent et peuvent afficher les données de salutation et ceux qui le gérer, mais ne doit pas avoir accès tooit.

#### <a name="cellcolumn-level-encryption"></a>Chiffrement au niveau des colonnes/cellules

Base de données SQL Azure vous permet de colonne de tooa tooapply symétrique de chiffrement de données à l’aide de Transact-SQL. Il s’agit [chiffrement au niveau colonne ou chiffrement au niveau de la cellule](https://docs.microsoft.com/sql/relational-databases/security/encryption/encrypt-a-column-of-data) (Effacer), car vous pouvez l’utiliser tooencrypt des colonnes spécifiques ou même des cellules de données avec différentes clés de chiffrement. Cela vous offre la possibilité d’un chiffrement plus granulaire que le chiffrement transparent des données, qui chiffre les données dans les pages.

CLE a des fonctions intégrées que vous pouvez utiliser les données de tooencrypt à l’aide des clés symétriques ou asymétriques, avec une clé publique d’un certificat hello, ou avec un mot de passe à l’aide de 3DES.

### <a name="cosmos-db-database-encryption"></a>Chiffrement de base de données Azure Cosmos DB

[Azure Cosmos DB](../cosmos-db/database-encryption-at-rest.md) est une base de données multi-modèles distribuée par Microsoft au niveau mondial. Données utilisateur stockées dans la base de données Cosmos dans le stockage non volatile (disques SSD) sont chiffrées par défaut ; Il n’y aucun tooturn contrôles ou la désactiver. Le chiffrement au repos est implémenté à l’aide d’un certain nombre de technologies de sécurité, notamment des systèmes de stockage de clés sécurisés, des réseaux chiffrés et des API de chiffrement. Les clés de chiffrement sont gérées par Microsoft et font l’objet d’une rotation par le biais de directives internes de Microsoft.

### <a name="at-rest-encryption-in-azure-data-lake"></a>Chiffrement au repos dans Azure Data Lake

[Azure Data Lake](../data-lake-store/data-lake-store-encryption.md) est un référentiel de l’entreprise de chaque type de données collectées dans une définition formelle de tooany préalable emplacement unique d’exigences ou de schéma. Prend en charge par Azure Data Lake Store » sur par défaut, « chiffrement transparent des données au repos, ce qui est défini lors de la création de hello de votre compte. Par défaut, Data Lake Store gère les clés de hello pour vous, mais vous avez hello option toomanage les vous-même.

Trois types de clés sont utilisés dans le chiffrement et le déchiffrement des données : hello clé de chiffrement principale (MEK), clé de chiffrement de données (DEK) et clé de chiffrement de blocs (BEK). Hello MEK est utilisé tooencrypt hello DEK, qui est stocké sur un support persistant, et hello BEK est dérivée de hello DEK et bloc de données hello. Si vous gérez vos propres clés, vous pouvez faire pivoter hello MEK.

## <a name="encryption-of-data-in-transit"></a>Chiffrement des données en transit

Azure offre plusieurs mécanismes pour protéger la confidentialité des données depuis un emplacement tooanother.

### <a name="tlsssl-encryption-in-azure"></a>Chiffrement TLS/SSL dans Azure

Microsoft utilise hello [Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) de protocole tooprotect données lorsqu’il est en déplacement entre les clients et les services de cloud computing hello. Centres de données de Microsoft négocient une connexion TLS avec les systèmes clients qui se connectent tooAzure services. TLS fournit une authentification forte, la confidentialité et l’intégrité des messages (activation de la détection de falsification, l’interception et la falsification des messages), l’interopérabilité, la flexibilité, la facilité de déploiement et l’utilisation des algorithmes.

[Perfect Forward Secrecy](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS) protège les connexions entre les systèmes clients des clients et les services cloud de Microsoft par des clés uniques. Les connexions utilisent également les longueurs de clés de chiffrement RSA de 2 048 bits. Cette combinaison rend difficile pour quelqu'un toointercept et accès aux données en transit.

### <a name="azure-storage-transactions"></a>Transactions de stockage Azure

Lorsque vous interagissez avec le stockage Azure via hello portail Azure, toutes les transactions aient lieu sur HTTPS. Vous pouvez également utiliser l’API REST de stockage de hello via HTTPS toointeract avec le stockage Azure. Vous pouvez appliquer utilisation hello du protocole HTTPS lors de l’appel d’objets de tooaccess d’API REST hello dans les comptes de stockage en activant un transfert sécurisé requis pour le compte de stockage hello.

Signatures d’accès partagé ([SAS](../storage/storage-dotnet-shared-access-signature-part-1.md)), qui peut être utilisé toodelegate accéder aux objets de stockage tooAzure, inclure une option toospecify que hello uniquement le protocole HTTPS peut être utilisé lors de l’utilisation de Signatures d’accès partagé. Cela garantit que toute personne envoyant des liens avec des jetons SAS utilise le protocole approprié de hello.

[SMB 3.0](https://technet.microsoft.com/library/dn551363(v=ws.11).aspx#BKMK_SMBEncryption) tooaccess utilisé des partages de fichiers Azure prend en charge le chiffrement, et il est disponible dans Windows Server 2012 R2, Windows 8, Windows 8.1 et Windows 10, ce qui permet l’accès entre régions et même accéder au bureau de hello.

Le chiffrement côté client chiffre les données de hello avant qu’il a envoyé tooAzure stockage, afin qu’il est chiffré lorsqu’il transite réseau hello.

### <a name="smb-encryption-over-azure-virtual-networks"></a>Chiffrement SMB sur les réseaux virtuels Azure 

[SMB 3.0](https://support.microsoft.com/help/2709568/new-smb-3-0-features-in-the-windows-server-2012-file-server) dans des machines virtuelles Azure exécutant Windows Server 2012 et ultérieur donne hello de données toomake de capacité sécuriser les transferts en chiffrant les données en transit sur les réseaux virtuels Azure, tooprotect contre la falsification et l’espionnage des attaques. Les administrateurs peuvent activer le chiffrement SMB pour l’ensemble du serveur hello ou des partages spécifiques.

Par défaut, une fois que le chiffrement SMB est activé pour un partage ou un serveur, seuls les clients SMB 3 sont autorisés tooaccess hello chiffré partages.

## <a name="in-transit-encryption-in-azure-virtual-machines"></a>Chiffrement en transit dans les machines virtuelles Azure

Données en transit entre les machines virtuelles Azure exécutant Windows vers et à partir de sont chiffrées dans un nombre de façons, selon la nature hello de connexion de hello.

### <a name="rdp-sessions"></a>Sessions RDP

Vous pouvez vous connecter et tooan session de machine virtuelle Azure à l’aide de hello [Remote Desktop Protocol](https://msdn.microsoft.com/library/aa383015(v=vs.85).aspx) (RDP) à partir d’un ordinateur client Windows, ou à partir d’un Mac avec un client RDP installé. Données en transit sur le réseau de hello dans les sessions RDP peuvent être protégées par le TLS.

Vous pouvez également utiliser le Bureau à distance tooconnect tooa Linux VM dans Azure.

### <a name="secure-access-toolinux-vms-with-ssh"></a>Sécuriser l’accès aux ordinateurs virtuels de tooLinux avec SSH

Vous pouvez utiliser [Secure Shell](../virtual-machines/linux/ssh-from-windows.md) (SSH) tooconnect tooLinux machines virtuelles s’exécutant dans Azure pour la gestion à distance. SSH est un protocole de connexion chiffré qui permet d'ouvrir des sessions en toute sécurité à travers des connexions non sécurisées. Il est le protocole de connexion par défaut hello pour les machines virtuelles Linux hébergés dans Azure. À l’aide de clés SSH pour l’authentification, vous inutiles hello pour toolog des mots de passe dans. SSH utilise une paire de clés publique/privée (chiffrement asymétrique) pour l’authentification.

## <a name="azure-vpn-encryption"></a>Chiffrement VPN Azure

Vous pouvez vous connecter à tooAzure via un réseau privé virtuel qui crée une tunnel sécurisé tooprotect hello une confidentialité des données hello qui sont envoyées sur le réseau de hello.

### <a name="azure-vpn-gateway"></a>Passerelle VPN Azure

[Passerelle VPN Azure](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md) peut être utilisé toosend chiffré le trafic entre votre réseau virtuel et votre emplacement local via une connexion publique, ou toosend entre les réseaux virtuels.

Le VPN de site à site utilise [IPsec](https://en.wikipedia.org/wiki/IPsec) pour le chiffrement du transport. Les passerelles VPN Azure utilisent un ensemble de propositions par défaut. Vous pouvez configurer toouse des passerelles VPN Azure à une stratégie IPsec/IKE personnalisée avec les algorithmes de chiffrement spécifiques et des avantages clés, plutôt que hello jeux de stratégie par défaut Azure.

### <a name="point-to-site-vpn"></a>VPN de point à site

Point-to-Site VPN permettre aux ordinateurs clients individuels accéder tooan réseau virtuel Azure. [Hello Secure Socket Tunneling Protocol](https://technet.microsoft.com/library/2007.06.cableguy.aspx) (SSTP) est le tunnel VPN de hello toocreate utilisé et peut traverser les pare-feux (tunnel de hello apparaît comme une connexion HTTPS). Puis-je utiliser ma propre AC racine PKI interne pour une connectivité de point à site.

Vous pouvez configurer un réseau de tooa virtuel point-to-site VPN connexion à l’aide de hello portail Azure avec l’authentification par certificat ou de PowerShell.

toolearn en savoir plus sur le point-to-site VPN connexions tooAzure des réseaux virtuels, consultez : [configurer un tooa de connexion de Point-to-Site réseau virtuel à l’aide de l’authentification de certification : portail Azure](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md) et

[Configurer un tooa de connexion de Point-to-Site réseau virtuel à l’aide de l’authentification par certificat : PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

### <a name="site-to-site-vpn"></a>VPN de site à site 

Une connexion de passerelle VPN de Site à Site est utilisé tooconnect votre site réseau tooan réseau virtuel Azure via un tunnel VPN de IPsec/IKE (IKEv1 ou IKEv2). Ce type de connexion requiert un VPN périphérique local qui a un tooit d’adresse IP publique externe.

Vous pouvez configurer un réseau de tooa virtuel site à site VPN connexion à l’aide de hello portail Azure, PowerShell ou hello Azure Interface de ligne de commande (CLI).

Veuillez lire ces informations supplémentaires :

[Créer une connexion de Site à Site dans hello portail Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

[Créer une connexion de site à site](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

[Créer un réseau virtuel avec une connexion VPN de site à site à l’aide de l’interface CLI](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="in-transit-encryption-in-azure-data-lake"></a>Chiffrement en transit dans Azure Data Lake

Les données en transit (ou données en mouvement) sont également toujours chiffrées dans Data Lake Store. En outre tooencrypting données toostoring préalable toopersistent média, les données de salutation sont également toujours protégées en transit à l’aide de HTTPS. HTTPS est hello seul protocole pris en charge pour hello que REST de magasin de données Lake interfaces.

toolearn en savoir plus sur le chiffrement des données en transit dans Azure Data Lake, consultez le document intitulé hello [chiffrement des données dans Azure Data Lake Store.](../data-lake-store/data-lake-store-encryption.md)

## <a name="key-management-with-azure-key-vault"></a>Gestion des clés dans Azure Key Vault

Sans la protection et la gestion des clés de hello, le chiffrement est inutilisable. Coffre de clés Azure est la solution recommandée de Microsoft pour gérer et contrôler les clés d’accès tooencryption utilisés par les services de cloud computing. Clés de tooaccess autorisations peuvent être attribués tooservices ou toousers via des comptes Azure Active Directory.

Coffre de clés Azure permet aux organisations de hello nécessité tooconfigure, de corriger et de mettre à jour les Modules de sécurité matériel (HSM) et le logiciel de gestion de clés. Avec Azure Key Vault, Microsoft ne voit jamais vos clés et les applications n’ont pas un accès direct toothem ; vous conservez le contrôle. Vous pouvez également importer ou générer des clés dans les modules HSM.

## <a name="next-steps"></a>Étapes suivantes

- [Vue d’ensemble de la sécurité d’Azure](security-get-started-overview.md)
- [Vue d’ensemble de la sécurité réseau d’Azure](security-network-overview.md)
- [Vue d’ensemble de la sécurité des bases de données d’Azure](azure-database-security-overview.md)
- [Vue d’ensemble de la sécurité des machines virtuelles d’Azure](security-virtual-machines-overview.md)
- [Chiffrement des données au repos](azure-security-encryption-atrest.md)
- [Meilleures pratiques en matière de chiffrement et de sécurité des données](azure-security-data-encryption-best-practices.md)
