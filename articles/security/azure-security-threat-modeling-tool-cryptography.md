---
title: "aaaCryptography - outil de modélisation des menaces Microsoft - Azure | Documents Microsoft"
description: "mesures d’atténuation des menaces exposé Bonjour outil de modélisation des menaces"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: cab981bf116a0e76bbf44fe0f0a1a3650e4ab0f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-cryptography--mitigations"></a>Infrastructure de sécurité : Chiffrement | Mesures de correction 
| Produit/Service | Article |
| --------------- | ------- |
| **Application web** | <ul><li>[Utiliser uniquement les longueurs de clé et les chiffrements par bloc symétriques approuvés](#cipher-length)</li><li>[Utiliser les modes de chiffrement par bloc et les vecteurs d’initialisation pour les chiffrements symétriques approuvés](#vector-ciphers)</li><li>[Utiliser les algorithmes asymétriques, les longueurs de clé et le remplissage approuvés](#padding)</li><li>[Utiliser les générateurs de nombres aléatoires approuvés](#numgen)</li><li>[Ne pas utiliser les chiffrements de flux symétriques](#stream-ciphers)</li><li>[Utiliser les algorithmes de hachage MAC/HMAC/indexé approuvés](#mac-hash)</li><li>[Utiliser uniquement les fonctions de hachage de chiffrement approuvées](#hash-functions)</li></ul> |
| **Base de données** | <ul><li>[Utiliser les données de tooencrypt les algorithmes de chiffrement renforcé dans la base de données hello](#strong-db)</li><li>[Les packages SSIS doivent être chiffrés et signés numériquement](#ssis-signed)</li><li>[Ajouter des éléments sécurisables de signature numérique toocritical base de données](#securables-db)</li><li>[Utiliser des clés de chiffrement SQL server EKM tooprotect](#ekm-keys)</li><li>[Utiliser la fonctionnalité de AlwaysEncrypted si les clés de chiffrement ne doivent pas être révélées tooDatabase moteur](#keys-engine)</li></ul> |
| **Appareil IoT** | <ul><li>[Stocker les clés de chiffrement façon sécurisée sur IoT Device](#keys-iot)</li></ul> | 
| **Passerelle de cloud IoT** | <ul><li>[Générer une clé symétrique aléatoire de longueur suffisante pour l’authentification tooIoT Hub](#random-hub)</li></ul> | 
| **Client mobile Dynamics CRM** | <ul><li>[Garantir qu’une stratégie de gestion des appareils, demandant un code confidentiel utilisateur et permettant la réinitialisation à distance, est en place](#pin-remote)</li></ul> | 
| **Client Outlook Dynamics CRM** | <ul><li>[Garantir qu’une stratégie de gestion des appareils, demandant un code confidentiel/mot de passe/verrouillage auto et chiffrant toutes les données (p. ex. Bitlocker), est en place](#bitlocker)</li></ul> | 
| **IdentityServer** | <ul><li>[Garantir que les clés de signature sont annulées lors de l’utilisation d’IdentityServer](#rolled-server)</li><li>[Garantir qu’un ID de client et une clé secrète client forts en termes de chiffrement sont utilisés dans IdentityServer](#client-server)</li></ul> | 

## <a id="cipher-length"></a>Utiliser uniquement les longueurs de clé et les chiffrements par bloc symétriques approuvés

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | <p>Produits doivent utiliser uniquement les chiffrements par bloc symétrique et les longueurs de clé associées qui ont été approuvés à hello Crypto Advisor dans votre organisation. Les algorithmes symétriques approuvés chez Microsoft incluent hello suivant le chiffrement par blocs :</p><ul><li>Pour le nouveau code, AES-128, AES-192 et AES-256 sont acceptables.</li><li>Pour la compatibilité descendante avec le code existant, 3DES avec trois clés est acceptable.</li><li>Pour les produits utilisant les chiffrements par bloc symétriques :<ul><li>Advanced Encryption Standard (AES) est requis pour le nouveau code.</li><li>Triple Data Encryption Standard (3DES) avec trois clés est autorisé dans le code existant pour la compatibilité descendante.</li><li>Tous les autres chiffrements par bloc, notamment RC2, DES, 3DES avec 2 clés, DESX et Skipjack, peuvent uniquement être utilisés pour le déchiffrement des données anciennes et doivent être remplacés en cas d’utilisation pour le chiffrement.</li></ul></li><li>Pour les algorithmes de chiffrement par bloc symétrique, une longueur de clé minimale de 128 bits est requise. Hello uniquement l’algorithme de chiffrement de blocs recommandé pour le nouveau code est AES (AES-128, AES-192 et AES-256 sont toutes acceptables)</li><li>Trois clé 3DES est actuellement acceptable si elles déjà en cours d’utilisation dans le code existant ; transition tooAES est recommandé. DES, DESX, RC2 et Skipjack ne sont plus considérés comme sûrs. Ces algorithmes peuvent uniquement être utilisés pour le déchiffrement des données existantes par souci de hello de compatibilité descendante et les données doivent être chiffrées de nouveau à l’aide d’un chiffrement par blocs recommandée</li></ul><p>Notez que tous les chiffrements par bloc symétriques doivent être utilisés avec un mode de chiffrement approuvé, ce qui nécessite l’utilisation d’un vecteur d’initialisation approprié. Un vecteur d’initialisation approprié est généralement un nombre aléatoire et jamais une valeur constante.</p><p>utilisation de Hello de hérités ou sinon algorithmes de chiffrement non approuvés et des longueurs de clé plus petites pour la lecture des données existantes (comme toowriting opposés de nouvelles données) peut être autorisée après révision de la carte de chiffrement de votre organisation. Toutefois, vous devez demander une exception à cette exigence. En outre, dans les déploiements d’entreprise, les produits doivent tenir compte administrateurs d’avertissement chiffrement faible est utilisé tooread données. Ces avertissements doivent être explicatifs et exploitables. Dans certains cas, il peut être utilisé de hello de contrôle de stratégie de groupe toohave approprié de chiffrement faible</p><p>Algorithmes .NET autorisés pour l’agilité de chiffrement géré (par ordre de préférence)</p><ul><li>AesCng (compatible FIPS)</li><li>AuthenticatedAesCng (compatible FIPS)</li><li>AESCryptoServiceProvider (compatible FIPS)</li><li>AESManaged (non compatible FIPS)</li></ul><p>Notez qu’aucune de ces algorithmes peut être spécifié via hello `SymmetricAlgorithm.Create` ou `CryptoConfig.CreateFromName` méthodes sans apporter de fichier des modifications toohello de machine.config. En outre, notez que AES dans les versions de too.NET préalable de .NET 3.5 est nommée `RijndaelManaged`, et `AesCng` et `AuthenticatedAesCng` sont > disponibles via CodePlex et doivent utiliser CNG hello sous-jacente du système d’exploitation</p>

## <a id="vector-ciphers"></a>Utiliser les modes de chiffrement par bloc et les vecteurs d’initialisation pour les chiffrements symétriques approuvés

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Tous les chiffrements par bloc symétriques doivent être utilisés avec un mode de chiffrement symétrique approuvé. modes de Hello uniquement approuvée sont CBC et CTS. En particulier, mode d’opération book (ECB) de code électronique hello doit être évité ; utilisation de ECB nécessite révision du tableau de chiffrement de votre organisation. Toute utilisation d’OFB, de CFB, de CTR, de CCM et de GCM ou de tout autre mode de chiffrement doit être examiné par le comité responsable du chiffrement de votre organisation. Réutilisation hello même vecteur d’initialisation (IV) avec le chiffrement par blocs dans « diffusion en continu les chiffrements de modes, » comme CTR, peut entraîner des toobe les données chiffrées qui s’affiché. Tous les chiffrements par bloc symétriques doivent également être utilisés avec un vecteur d’initialisation approprié. Un vecteur d’initialisation approprié est généralement un nombre aléatoire fort et jamais une valeur constante. |

## <a id="padding"></a>Utiliser les algorithmes asymétriques, les longueurs de clé et le remplissage approuvés

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | <p>Utilisez Hello interdits d’algorithmes de chiffrement présente la sécurité de tooproduct risque significatif et doit être évitée. Les produits doivent utiliser uniquement ces algorithmes de chiffrement ainsi que les longueurs de clé et le remplissage associés qui ont été approuvés explicitement par le comité responsable du chiffrement de votre organisation.</p><ul><li>**RSA-** peut être utilisé pour le chiffrement, la signature et l’échange de clés. Le chiffrement RSA doit utiliser uniquement hello OAEP ou RSA-KEM modes de remplissage. Le code existant peut utiliser le mode de remplissage PKCS #1 v1.5 à des fins de compatibilité uniquement. L’utilisation du remplissage nul est explicitement interdite. Des clés supérieures ou égales à 2 048 bits sont requises pour le nouveau code. Le code existant peut prendre en charge des clés inférieures à 2 048 bits uniquement à des fins de compatibilité descendante après un examen par le comité responsable du chiffrement de votre organisation. Des clés inférieures à 1 024 bits peuvent uniquement être utilisées pour le déchiffrement/la vérification d’anciennes données et doivent être remplacées si elles sont utilisées pour des opérations de chiffrement ou de signature.</li><li>**ECDSA-** peut être utilisé pour la signature uniquement. ECDSA avec des clés supérieures ou égales à 256 bits est requis pour le nouveau code. Les signatures ECDSA doivent utiliser une des courbes NIST approuvé hello trois (p-256, p-384 ou P521). Les courbes qui ont été rigoureusement analysées peuvent être utilisées uniquement après un examen du comité responsable du chiffrement de votre organisation.</li><li>**ECDH-** peut être utilisé pour l’échange de clés uniquement. ECDH avec des clés supérieures ou égales à 256 bits est requis pour le nouveau code. Échange de clé ECDH doit utiliser une des courbes NIST approuvé hello trois (p-256, p-384 ou P521). Les courbes qui ont été rigoureusement analysées peuvent être utilisées uniquement après un examen du comité responsable du chiffrement de votre organisation.</li><li>**DSA-** peut être acceptable après examen et approbation du comité responsable du chiffrement de votre organisation. Contactez votre tooschedule de l’Assistant sécurité de révision du tableau de chiffrement de votre organisation. Si votre utilisation du DSA est approuvée, notez que vous devez utiliser tooprohibit des clés de longueur inférieure à 2 048 bits. CNG prend en charge des longueurs de clé de 2 048 bits et supérieures à compter de Windows 8.</li><li>**Diffie-Hellman-** peut être utilisé pour la gestion des clés de session uniquement. Des longueurs de clé supérieures ou égales à 2 048 bits sont requises pour le nouveau code. Le code existant peut prendre en charge des longueurs de clé inférieures à 2048 bits uniquement à des fins de compatibilité descendante après un examen par le comité responsable du chiffrement de votre organisation. Des clés inférieures à 1 024 bits ne peuvent pas être utilisées.</li><ul>

## <a id="numgen"></a>Utiliser les générateurs de nombres aléatoires approuvés

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | <p>Les produits doivent utiliser les générateurs de nombres aléatoires approuvés. Les fonctions telles que rand de fonction hello C runtime, classe de .NET Framework hello System.Random ou fonctions système comme GetTickCount pseudo-aléatoire doivent, par conséquent, jamais utilisées dans ce code. Utilisation de hello à courbe elliptique double aléatoire algorithme Générateur de nombre (DUAL_EC_DRBG) est interdite.</p><ul><li>**CNG -** BCryptGenRandom (utilisation de l’indicateur BCRYPT_USE_SYSTEM_PREFERRED_RNG hello recommandé, sauf si l’appelant de hello peut-être s’exécuter sur n’importe quel IRQL supérieur à 0 [c'est-à-dire PASSIVE_LEVEL])</li><li>**CAPI-** cryptGenRandom.</li><li>**Win32/64-** RtlGenRandom (les nouvelles implémentations doivent utiliser BCryptGenRandom ou CryptGenRandom) * rand_s * SystemPrng (pour le mode noyau).</li><li>**.NET-** RNGCryptoServiceProvider ou RNGCng.</li><li>**Applications du Windows Store-** Windows.Security.Cryptography.CryptographicBuffer.GenerateRandom ou .GenerateRandomNumber.</li><li>**Apple OS X (10.7+)/iOS(2.0+) -** int SecRandomCopyBytes (SecRandomRef aléatoire, le nombre de size_t, uint8_t *octets)</li><li>**Apple OS X (< 10.7)-** utilisez / dev/aléatoire tooretrieve des nombres aléatoires</li><li>**Java (y compris le code Java Google Android)-** java.security.SecureRandom class. Notez que Android 4.3 (Bean gelée), les développeurs doivent suivre hello Android recommandé de solution de contournement et mettre à jour leur tooexplicitly applications initialiser hello PRNG avec entropie de /dev/urandom ou/dev/Random</li></ul>|

## <a id="stream-ciphers"></a>Ne pas utiliser les chiffrements de flux symétriques

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Les chiffrements de flux symétriques, tels que RC4, ne doivent pas être utilisés. Au lieu des chiffrements de flux symétriques, les produits doivent utiliser un chiffrement par bloc, en particulier AES avec une longueur de clé d’au moins 128 bits. |

## <a id="mac-hash"></a>Utiliser les algorithmes de hachage MAC/HMAC/indexé approuvés

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | <p>Les produits doivent utiliser uniquement le code d’authentification de message (MAC) approuvé ou des algorithmes de code d’authentification de message basé sur le hachage (HMAC).</p><p>Un code d’authentification de message (MAC) est une partie de message joint tooa d’information qui permet son destinataire tooverify les authenticité hello d’expéditeur de hello et intégrité hello de message de type hello à l’aide d’une clé secrète. Hello d’utilisation d’un MAC en fonction de hachage ([HMAC](http://csrc.nist.gov/publications/nistpubs/800-107-rev1/sp800-107-rev1.pdf)) ou [bloc cipher-basée sur un MAC](http://csrc.nist.gov/publications/nistpubs/800-38B/SP_800-38B.pdf) est autorisée tant que hachage tout sous-jacent ou les algorithmes de chiffrement symétrique sont également approuvés pour une utilisation ; actuellement ce inclut hello fonctions HMAC-SHA2 (HMAC-SHA256, SHA384-HMAC et HMAC-SHA512) et hello CMAC/OMAC1 et OMAC2 bloquent Mac en fonction de chiffrement (basées sur AES).</p><p>Utilisation du code HMAC-SHA1 peut être autorisée pour la compatibilité de la plateforme, mais vous sera nécessaire toofile une procédure d’exception de toothis et subir une révision de chiffrement de votre organisation. Troncation d’accessible sans les codes HMAC à 128 bits n’est pas autorisée. Utilisation des données et client méthodes toohash une clé n’est pas approuvée et fait l’objet toouse préalable de la révision de votre organisation du tableau de chiffrement.</p>|

## <a id="hash-functions"></a>Utiliser uniquement les fonctions de hachage de chiffrement approuvées

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | <p>Produits doivent utiliser la famille hello SHA-2 des algorithmes de hachage (SHA256, SHA384 et SHA512). Si un hachage plus court est nécessaire, notamment la longueur de la sortie de 128 bits dans l’ordre toofit une structure de données conçue avec hachage MD5 plus courte de hello à l’esprit, les équipes produit peuvent tronquer un des hachages de SHA2 hello (généralement SHA256). Notez que SHA384 est une version tronquée de SHA512. Troncation des hachages de chiffrement pour accessible sans à des fins de sécurité à 128 bits n’est pas autorisée. Nouveau code ne doit pas utiliser les algorithmes de hachage MD2, MD4, MD5, SHA-0, SHA-1 ou RIPEMD hello. Les conflits de hachage sont possibles en termes de calculs pour ces algorithmes, qui les brisent efficacement.</p><p>Algorithmes de hachage .NET autorisés pour l’agilité de chiffrement géré (par ordre de préférence) :</p><ul><li>SHA512Cng (compatible FIPS)</li><li>SHA384Cng (compatible FIPS)</li><li>SHA256Cng (compatible FIPS)</li><li>SHA512Managed (non conforme à FIPS) (utilisez SHA512 comme nom de l’algorithme dans les appels tooHashAlgorithm.Create ou CryptoConfig.CreateFromName)</li><li>SHA384Managed (non conforme à FIPS) (utilisez SHA384 comme nom de l’algorithme dans les appels tooHashAlgorithm.Create ou CryptoConfig.CreateFromName)</li><li>SHA256Managed (non conforme à FIPS) (utilisez SHA256 comme nom de l’algorithme dans les appels tooHashAlgorithm.Create ou CryptoConfig.CreateFromName)</li><li>SHA512CryptoServiceProvider (compatible FIPS)</li><li>SHA256CryptoServiceProvider (compatible FIPS)</li><li>SHA384CryptoServiceProvider (compatible FIPS)</li></ul>| 

## <a id="strong-db"></a>Utiliser les données de tooencrypt les algorithmes de chiffrement renforcé dans la base de données hello

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Base de données | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Choisir un algorithme de chiffrement](https://technet.microsoft.com/library/ms345262(v=sql.130).aspx) |
| **Étapes** | Les algorithmes de chiffrement définissent les transformations de données qui ne peuvent pas être facilement inversées par les utilisateurs non autorisés. SQL Server permet aux développeurs et administrateurs toochoose parmi plusieurs algorithmes, notamment DES, Triple DES, TRIPLE_DES_3KEY, RC2, RC4, RC4 128 bits, DESX, AES 128 bits, AES 192 bits et AES 256 bits |

## <a id="ssis-signed"></a>Les packages SSIS doivent être chiffrés et signés numériquement

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Base de données | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Identifier la Source de Packages avec des Signatures numériques de hello](https://msdn.microsoft.com/library/ms141174.aspx), [limitation des menaces et vulnérabilités (Integration Services)](https://msdn.microsoft.com/library/bb522559.aspx) |
| **Étapes** | source de Hello d’un package est hello individuel ou organisation qui a créé le package de hello. Exécuter un package à partir d’une source inconnue ou non fiable peut être dangereux. tooprevent non autorisé de falsification des packages SSIS, les signatures numériques doivent être utilisées. En outre, tooensure hello la confidentialité de packages hello pendant le stockage/transit, packages SSIS ont toobe chiffré |

## <a id="securables-db"></a>Ajouter des éléments sécurisables de signature numérique toocritical base de données

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Base de données | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [ADD SIGNATURE (Transact-SQL)](https://msdn.microsoft.com/library/ms181700) |
| **Étapes** | Dans les cas où l’intégrité de hello d’une base de données critiques sécurisable toobe vérifié, les signatures numériques doivent être utilisées. Les éléments sécurisables de base de données tels qu’une procédure stockée, une fonction, un assembly ou un déclencheur sont signés numériquement. Voici un exemple de lorsque cela peut être utile : supposons ISV (éditeurs de logiciels) a fourni la prise en charge tooa logiciel remis tooone de leurs clients. Avant de fournir la prise en charge, hello ISV souhaiteriez tooensure qu’un élément sécurisable dans le logiciel de hello de base de données n’a été pas été falsifié par inadvertance ou par une tentative malveillante. Si l’élément sécurisable de hello n’est pas signé numériquement, hello ISV peut vérifier sa signature numérique et valider leur intégrité.| 

## <a id="ekm-keys"></a>Utiliser des clés de chiffrement SQL server EKM tooprotect

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Base de données | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Gestion de clés extensible (EKM)](https://msdn.microsoft.com/library/bb895340), [Gestion de clés extensible à l’aide d’Azure Key Vault (SQL Server)](https://msdn.microsoft.com/library/dn198405) |
| **Étapes** | Gestion de clés Extensible de SQL Server Active les clés de chiffrement de hello qui protègent toobe de fichiers de base de données hello stockée dans un périphérique off-box comme une carte à puce, un périphérique USB ou un module EKM/HSM. Cela permet également la protection des données auprès des administrateurs de base de données (sauf les membres du groupe sysadmin de hello). Les données peuvent être chiffrées à l’aide de clés de chiffrement qu’uniquement hello utilisateur de base de données a module EKM/HSM externe d’accès tooon hello. |

## <a id="keys-engine"></a>Utiliser la fonctionnalité de AlwaysEncrypted si les clés de chiffrement ne doivent pas être révélées tooDatabase moteur

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Base de données | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | SQL Azure, OnPrem |
| **Attributs**              | Version SQL - V12, MsSQL2016 |
| **Informations de référence**              | [Always Encrypted (moteur de base de données)](https://msdn.microsoft.com/library/mt163865) |
| **Étapes** | Always Encrypted est une fonctionnalité conçue tooprotect les données sensibles, telles que les numéros de carte de crédit ou nationaux d’identification (par exemple, États-Unis numéros de sécurité sociale), stockées dans les bases de données de base de données SQL Azure ou SQL Server. Always Encrypted permet aux clients tooencrypt des données sensibles dans des applications clientes et ne jamais révéler toohello de clés de chiffrement hello du moteur de base de données (base de données SQL ou SQL Server). Par conséquent, la Always Encrypted fournit une séparation entre ceux qui possèdent des données de salutation (et peuvent les afficher) et ceux qui les gèrent les données de salutation (mais ne doivent avoir aucun accès) |

## <a id="keys-iot"></a>Stocker les clés de chiffrement de façon sécurisée sur IoT Device

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Appareil IoT | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | Système d’exploitation d’appareil - Windows IoT Standard, connectivité des appareils - Azure IoT device SDK |
| **Informations de référence**              | [TPM on Windows IoT Core](https://developer.microsoft.com/windows/iot/docs/tpm) (Module de plateforme sécurisée sur Windows IoT Standard), [TPM on Windows IoT Core](https://developer.microsoft.com/windows/iot/win10/setuptpm) (Module de plateforme sécurisée sur Windows IoT Standard), [Azure IoT Device SDK TPM](https://github.com/Azure/azure-iot-hub-vs-cs/wiki/Device-Provisioning-with-TPM) (Module de plateforme sécurisée Azure IoT Device SDK) |
| **Étapes** | Clés privées de certificat ou symétriques dans un stockage matériel protégé tel qu’un module de plateforme sécurisée ou des cartes à puce. Prend en charge de Windows 10 IoT Core utilisateur hello du module de plateforme sécurisée et qu’il existe plusieurs modules TPM compatible qui peut être utilisé : https://developer.microsoft.com/windows/iot/win10/tpm. Il est recommandé de toouse un microprogramme ou un TPM discrètes. Un module de plateforme sécurisée de type logiciel doit uniquement être utilisé à des fins de développement et de test. Une fois qu’un module de plateforme sécurisée est disponible et les clés de hello sont mis en service qu’il contient, code hello qui génère hello jeton doit être écrite sans codage dur toutes les informations sensibles qu’il contient. | 

### <a name="example"></a>Exemple
```
TpmDevice myDevice = new TpmDevice(0);
// Use logical device 0 on hello TPM 
string hubUri = myDevice.GetHostName(); 
string deviceId = myDevice.GetDeviceId(); 
string sasToken = myDevice.GetSASToken(); 

var deviceClient = DeviceClient.Create( hubUri, AuthenticationMethodFactory. CreateAuthenticationWithToken(deviceId, sasToken), TransportType.Amqp); 
```
Comme le montre, clé primaire du périphérique hello n’est pas présent dans le code hello. Au lieu de cela, il est stocké dans hello module de plateforme sécurisée à l’emplacement 0. Périphérique de module de plateforme sécurisée génère une courte durée de vie qui est ensuite utilisé tooconnect toohello IoT Hub. 

## <a id="random-hub"></a>Générer une clé symétrique aléatoire de longueur suffisante pour l’authentification tooIoT Hub

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Passerelle de cloud IoT | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | Choix de passerelle - Azure IoT Hub |
| **Informations de référence**              | N/A  |
| **Étapes** | IoT Hub contient un registre des identités de l’appareil et, lors de l’approvisionnement d’un appareil, il génère automatiquement une clé symétrique aléatoire. Il est recommandé de toouse cette fonctionnalité de hello Azure IoT Hub identité toogenerate hello clé utilisée pour l’authentification. IoT Hub permet également d’une clé toobe spécifié lors de la création de périphérique de hello. Si une clé est générée en dehors de IoT Hub lors de la configuration de l’appareil, il est recommandé de toocreate une clé symétrique aléatoire ou au moins de 256 bits. |

## <a id="pin-remote"></a>Garantir qu’une stratégie de gestion des appareils, demandant un code confidentiel utilisateur et permettant la réinitialisation à distance, est en place

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Client mobile Dynamics CRM | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Garantissez qu’une stratégie de gestion des appareils, demandant un code confidentiel utilisateur et permettant la réinitialisation à distance, est en place. |

## <a id="bitlocker"></a>Garantir qu’une stratégie de gestion des appareils, demandant un code confidentiel/mot de passe/verrouillage auto et chiffrant toutes les données (p. ex. Bitlocker), est en place

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Client Outlook Dynamics CRM | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Garantissez qu’une stratégie de gestion des appareils, demandant un code confidentiel/mot de passe/verrouillage auto et chiffrant toutes les données (p. ex. Bitlocker), est en place. |

## <a id="rolled-server"></a>Garantir que les clés de signature sont annulées lors de l’utilisation d’IdentityServer

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | IdentityServer | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [IdentityServer - Keys, Signatures and Cryptography ](https://identityserver.github.io/Documentation/docsv2/configuration/crypto.html) (IdentityServer - Clés, signatures et chiffrement) |
| **Étapes** | Garantissez que les clés de signature sont annulées lors de l’utilisation d’IdentityServer. lien de Hello dans la section des références hello explique comment cela doit être planifiée sans provoquer tooapplications pannes de partie de confiance sur le serveur d’identité. |

## <a id="client-server"></a>Garantir qu’un ID de client et une clé secrète client forts en termes de chiffrement sont utilisés dans IdentityServer

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | IdentityServer | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | <p>Garantir qu’un ID de client et une clé secrète client forts en termes de chiffrement sont utilisés dans IdentityServer. Hello instructions doit être utilisé lors de la génération d’un ID client et la clé secrète :</p><ul><li>Générer un GUID aléatoire en tant qu’ID de client hello</li><li>Générer une clé de 256 bits aléatoire par chiffrement en tant que secret de hello</li></ul>|
