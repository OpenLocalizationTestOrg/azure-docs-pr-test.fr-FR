---
title: "aaaAzure protéger les données personnelles au repos avec chiffrement | Documents Microsoft"
description: "Cet article fait partie d’une série de vous aider à utiliser les données personnelles tooprotect Azure"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 9af182b4897f1d04f5f519e6671f53b85073bae1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-at-rest-with-encryption"></a>technologies de chiffrement Azure : Protéger les données personnelles au repos avec un chiffrement

Cet article vous aidera à comprendre et utiliser les données de toosecure technologies Azure chiffrement au repos.

Chiffrement des données au repos est essentiel, comme une meilleure pratique tooprotect sensibles ou personnelles des données et la conformité de toomeet et exigences de confidentialité des données.
Chiffrement au repos est la personne malveillante de hello tooprevent conçu à partir de l’accès aux données de salutation non chiffrée en s’assurant que les données sont chiffrées sur le disque de hello.

## <a name="scenario"></a>Scénario 

Une société de croisière volumineux en hello États-Unis, étend ses itinéraires de toooffer d’opérations dans hello Méditerranée et mer Baltique, ainsi que hello britanniques. toosupport ces efforts, elle a acquis plusieurs lignes croisière plus petits dans Italie, Allemagne, Danemark et hello Royaume-Uni.

la société de Hello utilise des données d’entreprise de Microsoft Azure toostore dans le cloud de hello. Cela peut concerner des employés ou des informations sur les clients tels que :

- Adresses
- Numéros de téléphone
- Numéros d’identification fiscale
- informations médicales
- Informations de carte de crédit

société de Hello doit protection hello des données d’employé et client tout en effectuant des départements toothose accessible de données qui en ont besoin. (Notamment, les services de paie et de réservation.)

ligne de croisière Hello gère également les bases de données volumineuses de membres du programme de récompense et fidélité qui inclut des informations personnelles tootrack des relations avec les clients en cours et passées.

### <a name="problem-statement"></a>Définition du problème

société de Hello doit protection hello des employés et leurs données personnelles tout en effectuant des départements toothose accessible de données qui en ont besoin (par exemple, les services de paie et les réservations). Ces données sont stockées en dehors du centre de données d’entreprise hello et ne sont pas sous contrôle de la société hello physique.

### <a name="company-goal"></a>Objectif de l’entreprise

Dans le cadre d’une stratégie de sécurité de défense en profondeur multicouche, il s’agit d’un tooensure d’objectif de société que toutes les sources de données qui contiennent des données personnelles sont chiffrées, y compris ceux qui résident dans le stockage cloud. Si non autorisé personnes gain accès toohello données personnelles, il doit être dans un formulaire qui restituera illisible. L’application du chiffrement doit être simple (ou transparente) pour les utilisateurs et les administrateurs.

## <a name="solutions"></a>Solutions

Services Azure fournissent plusieurs toohelp d’outils et technologies vous protégez des données personnelles au repos en la chiffrant.

### <a name="azure-key-vault"></a>coffre de clés Azure

[Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) offre un stockage sécurisé pour les clés de hello utilisées tooencrypt données au repos dans les services Azure et hello est recommandé de solution de stockage et de gestion des clés. Gestion de clés de chiffrement toosecuring essentielles stockée donnée.

#### <a name="how-do-i-use-azure-key-vault-tooprotect-keys-that-encrypt-personal-data"></a>Utilisation de clés Azure Key Vault tooprotect chiffrement les données personnelles

toouse Azure Key Vault, vous devez un tooan abonnement compte Azure. Vous avez également besoin d’installer Azure PowerShell. Procédure : utilisation de PowerShell applets de commande toodo hello suit

1. Se connecter tooyour abonnements

2. Création d’un coffre de clés

3. Ajouter une clé ou un coffre de clés secrètes toohello

4. Inscrire des applications qui utiliseront le coffre de clés hello avec Azure Active Directory

5. Autoriser hello applications toouse hello clé ou le secret

toocreate un coffre de clés, utilisez hello applet de commande PowerShell New-AzureRmKeyVault. Vous devez attribuer un nom au coffre, un nom au groupe de ressources et un emplacement géographique. Vous allez utiliser le nom du coffre hello lors de la gestion des clés via d’autres applets de commande. Les applications qui utilisent le coffre hello via l’API REST de hello utilisera le coffre de hello URI.

Azure Key Vault peut vous fournir une clé protégée par un logiciel ou vous pouvez importer une clé existante dans un fichier .PFX. Vous pouvez également stocker des secrets (mots de passe) dans le coffre hello.

Vous pouvez également générer une clé dans votre HSM local et la transférez tooHSMs Bonjour service Key Vault, sans clé hello en laissant la limite HSM hello.

Pour obtenir des instructions détaillées sur l’utilisation d’Azure Key Vault, suivez les étapes hello [prise en main d’Azure Key Vault.](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)

Pour obtenir la liste des applets de commande PowerShell utilisées avec Azure Key Vault, consultez [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).

### <a name="azure-disk-encryption-for-windows"></a>Azure Disk Encryption pour Windows

[Azure Disk Encryption pour des machines virtuelles IaaS Windows et Linux](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) protège les données au repos sur les machines virtuelles Azure et s’intègre à Azure Key Vault. Le chiffrement des disques Azure utilise [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) dans Windows et [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) dans Linux tooencrypt deux hello des disques de données du système d’exploitation et hello. Azure Disk Encryption est pris en charge sur Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 et sur les clients Windows 8 et Windows 10.

#### <a name="how-do-i-use-azure-disk-encryption-tooprotect-personal-data"></a>Comment utiliser les données personnelles de chiffrement de disque Azure tooprotect ?

toouse chiffrement de disque Azure, vous devez un tooan abonnement compte Azure. Chiffrement tooenable Azure disque pour Windows et les machines virtuelles Linux, procédez comme hello suivant :

1. Utilisez le modèle de chiffrement de disque Azure Resource Manager hello, PowerShell ou le chiffrement de disque tooenable hello interface de ligne de commande (CLI) et spécifiez la configuration de chiffrement. 

2. Grant toohello d’accès matériel de chiffrement de plateforme Azure tooread hello dans votre coffre de clés.

3. Fournir un Azure Active Directory (AAD) application identité toowrite hello chiffrement tooyour matériel clé coffre de clés.

Azure sera mettre à jour hello machine virtuelle et la configuration du coffre de clés hello et configurer votre machine virtuelle chiffré.

Lorsque vous configurez votre toosupport de coffre de clés Azure un chiffrement de disque, vous pouvez ajouter une clé de chiffrement (KEK) pour renforcer la sécurité et de sauvegarde toosupport d’ordinateurs virtuels chiffrés.

![](media/protect-personal-data-at-rest/create-key.png)

Des instructions détaillées propres à des scénarios de déploiement et des expériences utilisateur spécifiques sont incluses dans [Azure Disk Encryption pour des machines virtuelles IaaS Windows et Linux.](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)

### <a name="azure-storage-service-encryption"></a>Chiffrement du service de stockage Azure

[Azure Storage Service de chiffrement (SSE) pour les données au repos](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) vous permet de protéger et de protéger votre toomeet données votre organisation engagements de conformité et de sécurité. Le stockage Azure automatiquement chiffre vos données à l’aide de toostorage de toopersisting préalable de chiffrement de AES 256 bits et la déchiffre tooretrieval préalable. Ce service est disponible pour les fichiers et objets blob Azure.

#### <a name="how-do-i-use-storage-service-encryption-tooprotect-personal-data"></a>Comment utiliser les données personnelles de chiffrement de Service de stockage tooprotect ?

tooenable chiffrement du Service de stockage, procédez comme hello suivant :

1. Connectez-vous à hello le portail Azure.

2. Sélectionnez un compte de stockage.

3. Dans Paramètres, sous la section du Service Blob hello, sélectionnez le chiffrement.

4. Hello service de fichiers, cliquez sur le chiffrement.

Une fois que vous cliquez sur le paramètre de chiffrement hello, vous pouvez activer ou désactiver le chiffrement de Service de stockage.

![](media/protect-personal-data-at-rest/storage-service-encryption.png)

Les nouvelles données sont chiffrées. Les données incluses dans les fichiers existants de ce compte de stockage restent non chiffrées.

Après l’activation du chiffrement, copiez le compte de stockage toohello de données à l’aide d’une des méthodes suivantes de hello :

1. Copier des objets BLOB ou fichiers avec hello [utilitaire de ligne de commande AzCopy](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy).

2. [Monter d’un partage de fichiers à l’aide de SMB](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows) afin de pouvoir utiliser un utilitaire tels que les fichiers de toocopy Robocopy.

3. Copier l’objet blob ou le fichier de données tooand depuis le stockage blob, ou entre des comptes de stockage à l’aide [bibliothèques clientes de stockage tels que .NET](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs).

4.  Utilisez un [Explorateur de stockage](https://docs.microsoft.com/en-us/azure/storage/storage-explorers) tooupload les objets BLOB de compte de stockage tooyour avec le chiffrement est activé.

### <a name="transparent-data-encryption"></a>Chiffrement transparent des données

Chiffrement transparent des données (TDE) est une fonctionnalité dans SQL Azure par lequel vous pouvez chiffrer les données aux deux niveaux de base de données et serveur hello. TDE est désormais activée par défaut sur toutes les nouvelles bases de données récemment créées. Chiffrement transparent des données effectue en temps réel d’e/s chiffrement et le déchiffrement des fichiers de données et journaux hello.

#### <a name="how-do-i-use-tde-tooprotect-personal-data"></a>Comment utiliser les données personnelles de chiffrement transparent des données tooprotect ?

Vous pouvez configurer le chiffrement transparent des données via hello portail Azure, à l’aide des API REST de hello, ou à l’aide de PowerShell. tooenable chiffrement transparent des données sur une base de données existante à l’aide de hello portail Azure, procédez comme hello suivant :

1. Visitez hello Azure portail à <https://portal.azure.com> et connectez-vous avec votre compte administrateur ou collaborateur Azure.

2. Sur la bannière de gauche hello, cliquez sur tooBROWSE, puis cliquez sur bases de données SQL.

3. Les bases de données SQL sélectionnée dans le volet gauche de hello, cliquez sur votre base de données utilisateur.

4. Dans le panneau de la base de données hello, cliquez sur tous les paramètres.

5. Dans le panneau des paramètres de hello, cliquez sur Panneau chiffrement Transparent des données de la tooopen partie Transparent des données chiffrement hello.

6. Dans le panneau de chiffrement de données hello, déplacez tooOn de bouton de chiffrement de données hello, puis cliquez sur Enregistrer (en hello haut hello) paramètre hello de tooapply. état du chiffrement de Hello indiquera approximativement la progression hello du chiffrement transparent des données de hello.

![Activation du chiffrement des données](media/protect-personal-data-at-rest/turn-data-encryption-on.png)

Instructions comment tooenable chiffrement transparent des données et des informations sur le déchiffrement de bases de données protégée par chiffrement transparent des données et d’informations peuvent être trouvée dans l’article de hello [chiffrement Transparent des données avec la base de données SQL Azure.](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)

## <a name="summary"></a>Résumé

société de Hello peut accomplir son objectif de chiffrement des données personnelles stockées dans hello cloud Azure. Cela à l’aide du chiffrement de disque Azure trop protéger des volumes entiers. Cela peut inclure des fichiers de système d’exploitation hello et les fichiers de données qui contiennent des informations d’identification personnelles et d’autres données sensibles. Chiffrement de Service de stockage Azure peut être tooprotect utilisé les données personnelles qui sont stockées dans les fichiers et les objets BLOB. Pour les données stockées dans des bases de données SQL Azure, Transparent Data Encryption fournit une protection contre l’exposition non autorisée des informations personnelles.

clés de hello tooprotect qui sont des données tooencrypt utilisés dans Azure, société de hello peut utiliser Azure Key Vault. Cela simplifie le processus de gestion de clés hello et Active hello contrôle toomaintain de société des clés d’accès et de chiffrer les données personnelles.

## <a name="next-steps"></a>Étapes suivantes

- [Guide de dépannage Azure Disk Encryption](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption-tsg)

- [Chiffrement d’une machine virtuelle Azure](https://docs.microsoft.com/en-us/azure/security-center/security-center-disk-encryption?toc=%2fazure%2fsecurity%2ftoc.json)

- [Chiffrement des données dans Azure Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)

- [Chiffrement de base de données Azure Cosmos DB au repos](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)
