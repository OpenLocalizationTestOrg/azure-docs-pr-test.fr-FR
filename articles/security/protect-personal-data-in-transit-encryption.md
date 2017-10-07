---
title: "aaaProtect des données personnelles en transit avec chiffrement dans Azure | Documents Microsoft"
description: "L’utilisation du chiffrement dans les données personnelles tooprotect Azure"
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
ms.openlocfilehash: 218ad3f49326e8dec299a6d92b18116da65eae71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-in-transit-with-encryption"></a>technologies de chiffrement Azure : Protéger les données personnelles en transit avec un chiffrement

Cet article vous aidera à comprendre et utiliser les données de toosecure de technologies de chiffrement Azure en transit. 

Protection confidentialité hello de données personnelles qu’il transite sur le réseau de hello est un élément essentiel d’une stratégie de sécurité de défense en profondeur multicouche. Le chiffrement en transit est conçue tooprevent une personne malveillante qui intercepte les transmissions d’être en mesure de données de hello tooview ou l’utilisation.

## <a name="scenario"></a>Scénario

Une société de croisière volumineux en hello États-Unis, étend ses itinéraires de toooffer d’opérations dans hello Méditerranée, Adriatique et mer Baltique, ainsi que hello britanniques. toosupport ces efforts, elle a acquis plusieurs lignes croisière plus petits exercées en Italie, Allemagne, Danemark et hello Royaume-Uni 

la société de Hello utilise des données d’entreprise de Microsoft Azure toostore dans le cloud de hello. Ces dernières incluent des informations d’identification personnelle telles que les noms, les adresses, les numéros de téléphone et les informations de carte de crédit de sa base de clients globale. Il inclut également des informations de ressources humaines traditionnelles telles que les adresses et numéros de téléphone, numéros d’identification de taxe médicales plus d’informations sur les employés de la société dans tous les emplacements. ligne de croisière Hello gère également les bases de données volumineuses de membres du programme de récompense et fidélité qui inclut des informations personnelles tootrack des relations avec les clients en cours et passées.

Les données personnelles de clients sont entrées dans la base de données hello à partir de sites distants de société hello et des agents de voyage dans Bonjour. Documents contenant des informations sur les clients sont transférées via le stockage de tooAzure réseau hello.

## <a name="problem-statement"></a>Définition du problème

société de Hello doit protéger la confidentialité de hello de clients et données personnelles de salariés pendant qu’il sont tooand de transit à partir des services Azure.

## <a name="company-goal"></a>Objectif de l’entreprise

Hello entreprise objectif tooensure que les données personnelles sont chiffrées lorsque sur disque. Si les personnes non autorisées interceptent les données personnelles de hello hors tension le disque, il doit être dans un formulaire qui restituera illisible. L’application du chiffrement doit être simple, ou entièrement transparent, pour les utilisateurs et les administrateurs.

## <a name="solutions"></a>Solutions

Services Azure fournissent plusieurs toohelp d’outils et technologies vous protégez des données personnelles en transit.

### <a name="azure-storage"></a>Azure Storage

Les données stockées dans le cloud de hello doivent être déplacée à partir du client hello, qui peut être physiquement situé n’importe où dans le centre de données Azure toohello, Bonjour tout le monde. Lorsque ces données sont récupérées par les utilisateurs, qu’elles soient à nouveau, Bonjour inverse le sens. Données en transit sur hello Internet public est toujours au risque d’interception par des personnes malveillantes. Il est confidentialité de hello tooprotect importantes de données personnelles à l’aide de toosecure de chiffrement au niveau du transport en tant qu’il se déplace entre les emplacements.

Hello le protocole HTTPS fournit un canal de communication sécurisé, chiffré sur hello Internet. HTTPS doivent être des objets de tooaccess utilisé dans le stockage Azure et lors de l’appel d’API REST. Appliquer d’utilisation du protocole HTTPS de hello lors de l’utilisation [Signatures d’accès partagé](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) (SAS) toodelegate tooAzure stockage DAO. Il existe deux types de SAP : SAP de service et SAP de compte.

#### <a name="how-do-i-construct-a-service-sas"></a>Comment construire une SAP de service ?

Une ressource Service SAS délégués accès tooa dans un seul des services de stockage hello (service blob, file d’attente, table ou de fichier). tooconstruct une SAP de Service, procédez comme hello suivant :

1. Spécifiez hello signé le champ de Version

2. Spécifiez hello ressource signée (objet Blob et fichier Service uniquement)

3. Spécifiez les paramètres de requête tooOverride les en-têtes de réponse (Service Blob et fichier Service uniquement)

4. Spécifiez hello nom de la Table (Table Service uniquement)

5. Spécifier la stratégie d’accès de hello

6. Spécifiez hello intervalle de validité de Signature

8. Spécifier des autorisations

9. Spécifier l’adresse IP ou la plage d’adresses IP

10. Spécifiez hello protocole HTTP

11. Spécifier les plages d’accès de Table

12. Spécifiez hello signé identificateur

13. Spécifiez hello Signature

Pour plus d’instructions, consultez [Construction d’une SAP de service](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN).

#### <a name="how-do-i-construct-an-account-sas"></a>Comment construire une SAP de compte ?

Un compte de SAS délègue tooresources d’accès dans une ou plusieurs des services de stockage hello. Vous pouvez également déléguer l’accès tooread, écriture et les opérations de suppression sur les conteneurs d’objets blob, tables, files d’attente et les partages de fichiers qui ne sont pas autorisées avec un service SAS. Construction d’une SAP de compte est toothat similaire d’un Service. Pour obtenir des instructions détaillées, consultez [Construction d’une SAP de compte.](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)

#### <a name="how-do-i-enforce-https-when-calling-rest-apis"></a>Comment mettre en place le protocole HTTPS lors de l’appel d’API REST ?

utilisation de hello tooenforce du protocole HTTPS lors de l’appel d’objets de tooaccess API REST de comptes de stockage, vous pouvez activer Secure transfert requis pour le compte de stockage hello. 

1. Bonjour portail Azure, sélectionnez **créer un compte de stockage**, ou pour un compte de stockage existant, sélectionnez **paramètres** , puis **Configuration**.

2. Sous **Transfert sécurisé requis**, sélectionnez **Activé**.

![Création d’un compte de stockage](media/protect-personal-data-in-transit-encryption/create-storage-account.png)

Pour plus d’instructions, y compris comment tooenable Secure transfert requis par programme, consultez [nécessitent un transfert de sécuriser](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).

#### <a name="how-do-i-encrypt-data-in-azure-file-storage"></a>Comment chiffrer des données dans Stockage Fichier Azure ?

tooencrypt des données en transit avec [stockage de fichiers Azure](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), vous pouvez utiliser SMB 3.x avec Windows 8, 8.1 et 10 et Windows Server 2012 R2 et Windows Server 2016. Lorsque vous utilisez le service de fichiers Azure hello, toute connexion sans chiffrement échoue lorsque « Sécuriser le transfert requis » est activée. Cela inclut des scénarios à l’aide de SMB 2.1, SMB 3.0 sans chiffrement et certaines versions de hello client Linux SMB.

#### <a name="azure-client-side-encryption"></a>Chiffrement côté client Azure

Une autre possibilité pour protéger des données personnelles pendant leur transfert entre une application cliente et Stockage Azure consiste à utiliser un [chiffrement côté client](https://docs.microsoft.com/azure/storage/storage-client-side-encryption). les données de salutation sont chiffrées avant d’être transférées dans le stockage Azure, et lorsque vous récupérez des données de hello depuis le stockage Azure, les données de salutation sont déchiffrées après sa réception côté client de hello.

### <a name="azure-site-to-site-vpn"></a>VPN de site à site Azure

Un moyen efficace tooprotect personnel de données en transit entre un réseau d’entreprise ou un utilisateur et un réseau virtuel Azure de hello sont toouse un [site-à-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) ou [point-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) réseau privé virtuel (VPN, Virtual Private Network). Une connexion VPN crée un tunnel chiffré sécurisé sur Internet de hello.

#### <a name="how-do-i-create-a-site-to-site-vpn-connection"></a>Comment créer une connexion VPN de site à site ?

Un VPN de site à site connecte à plusieurs utilisateurs sur tooAzure de réseau d’entreprise hello. toocreate une connexion site à site Bonjour portail Azure, procédez comme hello suivant :

1. Créez un réseau virtuel.

2. Spécifiez un serveur DNS.

3. Créer un sous-réseau de passerelle hello.

4. Créer la passerelle VPN de hello. 

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-01.png)

5. Créer la passerelle de réseau local hello.

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-02.png)

6. Configurez votre appareil VPN.

7. Créer un réseau VPN hello.

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-03.png)

8. Vérifiez la connexion VPN de hello.

Pour plus d’instructions sur la connexion toocreate un site à site dans hello Azure portail, consultez [connexion de la création d’un Site à Site Bonjour portail Azure.] (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)

#### <a name="how-do-i-create-a-point-to-site-vpn-connection"></a>Comment créer une connexion VPN de point à site ?

Un VPN de Point-to-Site crée une connexion sécurisée à partir d’un réseau virtuel du tooa d’ordinateur client individuel. Cela est utile lorsque vous souhaitez tooAzure tooconnect à partir d’un emplacement distant, par exemple à partir du centre d’accueil ou un hôtel ou d’une conférence. toocreate une connexion point-to-site Bonjour portail Azure,

1. Créez un réseau virtuel.

2. Ajoutez un sous-réseau de passerelle.

3. Spécifiez un serveur DNS. (facultatif)

4. Créez une passerelle de réseau virtuel.

5. Générez des certificats.

6. Ajouter un pool d’adresses client hello.

7. Télécharger les données de certificat public du certificat hello racine.

8. Générer et installer le package de configuration de client VPN hello.

9. Installez un certificat client exporté.

10. Se connecter tooAzure.

11. Vérifiez votre connexion.

Pour plus d’instructions, consultez [configurer un tooa de connexion de Point-to-Site réseau virtuel à l’aide de l’authentification par certificat : portail Azure.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)

### <a name="ssltls"></a>SSL/TLS

Microsoft vous recommande de toujours utiliser des données de tooexchange protocoles SSL/TLS sur les différents sites. Les organisations qui choisissez toouse [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) toomove de grands jeux de données sur une liaison WAN à haut débit dédiée peut également chiffrer les données hello hello pour une protection supplémentaire à l’aide de SSL/TLS ou autres protocoles de niveau application.

### <a name="encryption-by-default"></a>Chiffrement par défaut

Microsoft utilise les données de tooprotect de chiffrement en transit entre les clients et services de cloud computing Azure. Si vous interagissez avec le stockage Azure via hello portail Azure, toutes les transactions se produisent via HTTPS.

[Sécurité de la couche de transport](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) est le protocole hello que toonegotiate avec les systèmes clients qui se connectent à des services de cloud computing tooMicrosoft va tenter de centres de données Microsoft. TLS fournit une authentification forte, la confidentialité et l’intégrité des messages (activation de la détection de falsification, l’interception et la falsification des messages), l’interopérabilité, la flexibilité, la facilité de déploiement et l’utilisation des algorithmes.

[PFS (Perfect Forward Secrecy)](https://en.wikipedia.org/wiki/Forward_secrecy) est aussi utilisé pour que chaque connexion entre les systèmes clients des clients et les services cloud de Microsoft utilisent des clés uniques. Services de cloud computing connexions tooMicrosoft également tirer parti du chiffrement de 2 048 bits en fonction de RSA longueurs de clé. Hello combinaison de TLS, longueurs de clé RSA 2048 bits, et PFS rend beaucoup plus difficile pour une personne toointercept et l’accès des données en transit entre les clients et les services cloud Microsoft.

Les données en transit sont toujours chiffrées dans [Data Lake Store] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview). En outre tooencrypting données toostoring préalable toopersistent média, les données de salutation sont également toujours protégées en transit à l’aide de HTTPS. HTTPS est hello seul protocole pris en charge pour hello que REST de magasin de données Lake interfaces.

## <a name="summary"></a>Résumé

société de Hello peut accomplir son objectif de protection des données et hello confidentialité de ces données par l’application tooAzure des connexions HTTPS stockage, à l’aide de Signatures d’accès partagé et l’activation de Secure transfert requis sur les comptes de stockage hello. Elle peut aussi protéger les données personnelles en utilisant des connexions SMB 3.0 et en mettant en place un chiffrement côté client. Connexions VPN de site à site à partir de hello réseau d’entreprise toohello réseau virtuel Azure et les connexions VPN de point-to-site auprès des utilisateurs crée un tunnel sécurisé par le biais duquel peuvent voyager en toute sécurité des données personnelles. Pratiques de chiffrement par défaut de Microsoft protège davantage confidentialité hello des données personnelles.

## <a name="next-steps"></a>Étapes suivantes

- [Bonnes pratiques Azure en matière de chiffrement et de sécurité des données](https://docs.microsoft.com/azure/security/azure-security-data-encryption-best-practices)

- [Planification et conception de la passerelle VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)

- [FAQ sur la passerelle VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vpn-faq)

- [Acheter et configurer un certificat SSL pour votre service Azure App Service](https://docs.microsoft.com/azure/app-service-web/web-sites-purchase-ssl-web-site)
