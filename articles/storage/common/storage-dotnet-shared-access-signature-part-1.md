---
title: "aaaUsing partagé (SAS) des signatures d’accès dans le stockage Azure | Documents Microsoft"
description: "En savoir plus toouse partagé accès signatures (SAS) toodelegate accès tooAzure ressources de stockage, y compris les objets BLOB, les files d’attente, les tables et les fichiers."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 46fd99d7-36b3-4283-81e3-f214b29f1152
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/18/2017
ms.author: marsma
ms.openlocfilehash: 5b75a3c25bcfb9f1ceb81f31dc2d42376bd105cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-shared-access-signatures-sas"></a>Utilisation des signatures d’accès partagé (SAP)

Une signature d’accès partagé (SAS) vous offre un tooobjects d’accès toogrant limitée moyen dans votre compte de stockage tooother clients, sans exposer votre clé de compte. Dans cet article, nous fournissent une vue d’ensemble du modèle SAS hello, consulter les meilleures pratiques SAS et consulter des exemples.

Pour obtenir des exemples de code supplémentaire à l’aide de SAP au-delà de celles présentées ici, consultez [prise en main de stockage d’objets Blob Azure dans .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/) et d’autres exemples disponibles dans hello [exemples de Code Azure](https://azure.microsoft.com/documentation/samples/?service=storage) bibliothèque. Vous pouvez télécharger des exemples d’applications hello et les exécuter ou parcourir le code hello sur GitHub.

## <a name="what-is-a-shared-access-signature"></a>Présentation de la signature d’accès partagé
Une signature d’accès partagé fournit tooresources accès délégué dans votre compte de stockage. Avec une SAP, vous pouvez accorder les clients d’accès tooresources dans votre compte de stockage sans partager vos clés de compte. Il s’agit hello le point clé de l’utilisation de signatures d’accès partagé dans vos applications--une SAP est un tooshare de manière sécurisée à vos ressources de stockage sans compromettre vos clés de compte.

[!INCLUDE [storage-account-key-note-include](../../../includes/storage-account-key-note-include.md)]

Un SAS vous donne un contrôle précis sur le type de hello d’accès que vous accordez tooclients ayant hello SAP, y compris :

* intervalle de salutation sur quel hello SAS est valide, y compris l’heure de début hello et l’heure d’expiration de hello.
* autorisations de Hello accordées par hello SAS. Par exemple, un SAS pour un objet blob peut accorder en lecture et écriture autorisations toothat blob, mais pas supprimer des autorisations.
* Une adresse IP facultatif ou la plage d’adresses IP à partir de laquelle le stockage Azure acceptera hello SAS. Par exemple, vous pouvez spécifier une plage d’adresses IP appartenant tooyour organisation.
* protocole Hello sur lequel le stockage Azure acceptera hello SAS. Vous pouvez utiliser cette tooclients d’accès toorestrict paramètre facultatif à l’aide de HTTPS.

## <a name="when-should-you-use-a-shared-access-signature"></a>Quand devez-vous utiliser une signature d’accès partagé ?
Vous pouvez utiliser une SAP lorsque vous souhaitez tooprovide accès tooresources dans votre client de tooany de compte de stockage ne possédant ne pas de clés d’accès de votre compte de stockage. Votre compte de stockage inclut à la fois une clé d’accès primaire et secondaire, qui accorder le compte d’accès administratif tooyour et toutes les ressources qu’il contient. Exposition d’une de ces clés ouvre votre possibilité de toohello compte d’utilisation malveillante ou involontaire. Signatures d’accès partagé offrent une solution sécurisée qui permet aux clients tooread, écriture et suppression des données dans votre compte de stockage en fonction des autorisations toohello que vous avez accordé explicitement et sans besoin d’une clé de compte.

Un scénario courant où une SAP est utile est un service où les utilisateurs lire et écrire son propre compte de stockage de données tooyour. Dans un scénario où un compte de stockage stocke les données utilisateur, il existe deux modèles de conception types :

1. Les clients chargent et téléchargent les données par le biais d’un service proxy frontal, qui se charge de l’authentification. Ce service de proxy frontal a l’avantage hello de validation de règles d’entreprise, mais pour grandes quantités de données ou des transactions volumineuses, créez un service qui peut évoluer à la demande toomatch peut être difficile ou coûteuse.

  ![Schéma du scénario : service proxy frontal](./media/storage-dotnet-shared-access-signature-part-1/sas-storage-fe-proxy-service.png)   

1. Un service léger authentifie le client de hello en fonction des besoins et génère ensuite un SAS. Une fois que le client de hello reçoit hello SAS, ils peuvent accéder les ressources de compte de stockage directement avec les autorisations hello définies par hello SAP et pour intervalle hello autorisée par hello SAS. Hello SAS atténue la nécessité de hello pour le routage de toutes les données via le service de proxy frontal hello.

  ![Schéma du scénario : service du fournisseur SAP](./media/storage-dotnet-shared-access-signature-part-1/sas-storage-provider-service.png)   

De nombreux services réels peuvent utiliser un mélange de ces deux approches. Par exemple, certaines données peuvent être traitées et validées via le proxy frontal hello, alors que les autres données sont enregistrées et/ou lire directement à l’aide de SAP.

En outre, vous devez toouse un objet de source SAP tooauthenticate hello dans une opération de copie dans certains scénarios :

* Lorsque vous copiez un objet blob tooanother blob qui réside dans un autre compte de stockage, vous devez utiliser un objet blob de la source SAS tooauthenticate hello. Vous pouvez éventuellement utiliser un SAS tooauthenticate hello objet blob de destination ainsi.
* Lorsque vous copiez un fichier tooanother qui se trouve dans un autre compte de stockage, vous devez utiliser un fichier de source SAP tooauthenticate hello. Vous pouvez éventuellement utiliser un SAS tooauthenticate hello fichier de destination ainsi.
* Lorsque vous copiez un fichier de tooa blob ou d’un objet blob tooa de fichier, vous devez utiliser un objet de source SAP tooauthenticate hello, même si les objets source et destination hello résident dans hello même compte de stockage.

## <a name="types-of-shared-access-signatures"></a>Types de signatures d’accès partagé
Vous pouvez créer deux types de signatures d’accès partagé :

* **SAP de service.** les délégués SAS Hello service d’accès tooa des ressources dans un seul des services de stockage hello : hello service Blob, file d’attente, Table ou de fichier. Consultez [construction d’un SAS Service](https://msdn.microsoft.com/library/dn140255.aspx) et [Service SAS exemples](https://msdn.microsoft.com/library/dn140256.aspx) pour des informations détaillées sur la construction du jeton SAS du service hello.
* **SAP de compte.** les délégués SAS Hello compte d’accès tooresources dans un ou plusieurs des services de stockage hello. Toutes les opérations de hello disponibles via un service SAP sont également disponibles via un compte SAP. En outre, avec un compte hello SAS, vous pouvez déléguer toooperations access qui s’appliquent tooa donné de service, tel que **propriétés de Service Get/Set** et **obtenir des statistiques du Service**. Vous pouvez également déléguer l’accès tooread, écriture et les opérations de suppression sur les conteneurs d’objets blob, tables, files d’attente et les partages de fichiers qui ne sont pas autorisées avec un service SAS. Consultez [construction d’un SAS compte](https://msdn.microsoft.com/library/mt584140.aspx) pour des informations détaillées sur la construction d’un jeton SAS hello compte.

## <a name="how-a-shared-access-signature-works"></a>Fonctionnement d’une signature d’accès partagé
Une signature d’accès partagé est signé URI qui pointe tooone ou davantage de ressources de stockage et inclut un jeton qui contient un ensemble spécial de paramètres de requête. jeton de Hello indique comment les ressources hello est accessible par le client de hello. Un des paramètres de requête hello, hello signature est construite à partir des paramètres SAS hello et signé avec la clé de compte hello. Cette signature est utilisée par hello tooauthenticate de stockage Azure SAS.

Voici un exemple d’URI SAS, URI de ressource montrant hello et un jeton SAS hello :

![Composants d’un URI SAP](./media/storage-dotnet-shared-access-signature-part-1/sas-storage-uri.png)   

jeton SAS Hello est une chaîne que vous générez sur hello *client* côté (consultez hello [exemples SAS](#sas-examples) section d’exemples de code). Un jeton SAP que vous générez avec la bibliothèque cliente de stockage hello, par exemple, n'est pas suivi par le stockage Azure en aucune façon. Vous pouvez créer un nombre illimité de jetons SAP côté client de hello.

Lorsqu’un client fournit un tooAzure URI SAS du stockage dans le cadre d’une demande, service de hello vérifie les paramètres SAS hello et tooverify signature qu’il est valide pour authentifier la demande de hello. Si le service de hello vérifie qu’une signature hello est valide, la demande de hello est authentifié. Dans le cas contraire, demande de hello est refusée avec le code d’erreur 403 (interdit).

## <a name="shared-access-signature-parameters"></a>Paramètres de la signature d’accès partagé (SAP)
le compte de Hello SAS et de jetons SAS du service incluent des paramètres courants et également prennent quelques paramètres qui sont différentes.

### <a name="parameters-common-tooaccount-sas-and-service-sas-tokens"></a>Tooaccount commun de paramètres SAS et jetons SAS du service
* **Version de l’API** un paramètre facultatif qui spécifie hello stockage service version toouse tooexecute hello demande.
* **Version du service** un paramètre obligatoire qui spécifie hello stockage service version toouse tooauthenticate hello demande.
* **Heure de début.** Il s’agit de heure hello à quels hello SAS devient valide. heure de début Hello pour une signature d’accès partagé est facultative. Si une heure de début est omise, hello SAS prend effet immédiatement. Hello heure de début doit être exprimée en heure UTC (Coordinated Universal Time), avec un indicateur UTC spéciaux (« Z »), par exemple `1994-11-05T13:15:30Z`.
* **Heure d’expiration.** Il s’agit de hello heure après laquelle hello SAS n’est plus valide. Les meilleures pratiques recommandent soit de spécifier une heure d’expiration pour une signature d’accès partagé, soit de l’associer à une stratégie d’accès stockée. Hello délai d’expiration doit être exprimée en heure UTC (Coordinated Universal Time), avec un indicateur UTC spéciaux (« Z »), par exemple `1994-11-05T13:15:30Z` (voir ci-dessous).
* **Autorisations.** autorisations de Hello spécifiées sur hello SAS indiquent les opérations client de hello peut effectuer par rapport à la ressource de stockage hello à l’aide de hello SAS. Les autorisations disponibles ne sont pas les mêmes pour une SAP de compte et une SAP de service.
* **IP.** Un paramètre facultatif qui spécifie une adresse IP ou une plage d’adresses IP en dehors de Azure (consultez la section de hello [état de configuration de session de routage](../../expressroute/expressroute-workflows.md#routing-session-configuration-state) pour Express Route) à partir de quelles demandes tooaccept.
* **Protocole.** Un paramètre facultatif qui spécifie le protocole de hello autorisée pour une demande. Les valeurs possibles sont à la fois HTTP et HTTPS (`https,http`), qui est la valeur par défaut de hello ou HTTPS uniquement (`https`). Notez que HTTP uniquement n’est pas une valeur autorisée.
* **Signature.** signature de Hello est construit à partir de hello autres paramètres spécifié en tant que partie jeton, puis chiffrées. Il a utilisé tooauthenticate hello SAS.

### <a name="parameters-for-a-service-sas-token"></a>Paramètres d’un jeton de SAP de service
* **Ressource de stockage.** Les ressources de stockage dont vous pouvez déléguer l’accès à l’aide d’une SAP de service incluent :
  * Conteneurs et objets blob
  * Partages de fichiers et fichiers
  * Files d’attente
  * Tables et plages d’entités de table.

### <a name="parameters-for-an-account-sas-token"></a>Paramètres d’un jeton de compte SAP
* **Service ou services.** Un compte SAP peut déléguer l’accès tooone ou plusieurs des services de stockage hello. Par exemple, vous pouvez créer un compte SAP que délégués accéder au service d’objet Blob et le fichier toohello. Ou vous pouvez créer une SAP de délégués d’accès tooall quatre services (Blob, file d’attente, Table et fichier).
* **Types de ressources de stockage.** Un compte SAP s’applique tooone ou plusieurs classes de ressources de stockage, plutôt que d’une ressource spécifique. Vous pouvez créer un compte SAP toodelegate l’accès à :
  * API au niveau du service, qui sont appelées par rapport à la ressource de compte de stockage hello. Exemples : **Get/Set Service Properties**, **Get Service Stats** et **List Containers/Queues/Tables/Shares**.
  * API au niveau du conteneur, qui est appelées sur des objets conteneur hello pour chaque service : conteneurs, des files d’attente, des tableaux d’objets blob et les partages de fichiers. Exemples : **Create/Delete Container**, **Create/Delete Queue**, **Create/Delete Table**, **Create/Delete Share** et **List Blobs/Files and Directories**.
  * Des API au niveau de l’objet, qui sont appelées sur les objets blob, les messages de file d’attente, les entités de table et les fichiers. Exemples : **Put Blob**, **Query Entity**, **Get Messages** et **Create File**.

## <a name="examples-of-sas-uris"></a>Exemples d’URI de SAP

### <a name="service-sas-uri-example"></a>Exemple d’URI SAP de service

Voici un exemple d’un service qui fournit l’URI SAS lire et écrire des blob de tooa d’autorisations. table de Hello décompose chaque partie de hello URI toounderstand comment il contribue toohello SAS :

```
https://myaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2015-04-05&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D
```

| Nom | Partie de la SAP | Description |
| --- | --- | --- |
| URI de l’objet blob |`https://myaccount.blob.core.windows.net/sascontainer/sasblob.txt` |adresse Hello d’objet blob de hello. Notez que l'utilisation de HTTPS est fortement recommandée. |
| Version des services de stockage |`sv=2015-04-05` |Pour les services de stockage de la version 2012-02-12 et versions ultérieures, ce paramètre indique hello version toouse. |
| Heure de début |`st=2015-04-29T22%3A18%3A26Z` |Spécifiée en heure UTC. Si vous souhaitez hello SAS toobe valide immédiatement, omettez l’heure de début hello. |
| Heure d’expiration |`se=2015-04-30T02%3A23%3A26Z` |Spécifiée en heure UTC. |
| Ressource |`sr=b` |ressource de Hello est un objet blob. |
| Autorisations |`sp=rw` |autorisations de Hello en hello SAS incluent Read (r) et écriture (w). |
| Plage d’adresses IP |`sip=168.1.5.60-168.1.5.70` |Hello plage d’adresses IP à partir de laquelle une demande est acceptée. |
| Protocole |`spr=https` |Seules les demandes utilisant HTTPS sont autorisées. |
| Signature |`sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D` |Utilisé blob de toohello tooauthenticate accès. signature de Hello est un HMAC calculé sur une chaîne de signature et la clé à l’aide d’algorithme de hello SHA256, puis codé en Base64. |

### <a name="account-sas-uri-example"></a>Exemple d’URI SAP de compte

Voici un exemple d’un compte SAP qu’utilise hello les mêmes paramètres courants sur le jeton de hello. Dans la mesure où ces paramètres sont décrits ci-dessus, ils ne sont pas décrits ici. Seuls les paramètres hello qui sont spécifique tooaccount que SAP est décrits dans le tableau hello ci-dessous.

```
https://myaccount.blob.core.windows.net/?restype=service&comp=properties&sv=2015-04-05&ss=bf&srt=s&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=F%6GRVAZ5Cdj2Pw4tgU7IlSTkWgn7bUkkAg8P6HESXwmf%4B
```

| Nom | Partie de la SAP | Description |
| --- | --- | --- |
| URI de ressource |`https://myaccount.blob.core.windows.net/?restype=service&comp=properties` |Hello Blob service point de terminaison, avec des paramètres pour l’obtention des propriétés du service (lorsqu’il est appelé avec GET) ou de la définition des propriétés du service (lorsqu’il est appelé avec SET). |
| Services |`ss=bf` |Hello SAP s’applique toohello Blob et les services de fichiers |
| Types de ressources |`srt=s` |Hello SAP s’applique au niveau tooservice operations. |
| Autorisations |`sp=rw` |autorisations de Hello accorder l’accès tooread et les opérations d’écriture. |

Étant donné que les autorisations sont limitées au niveau du service toohello, opérations accessibles avec cette SAS sont **Get Blob Service Properties** (lecture) et **Set Blob Service Properties** (écriture). Toutefois, avec un URI de ressource différent, hello même jeton SAS peut également être utilisée de trop toodelegate accès**obtenir des statistiques du Service Blob** (lecture).

## <a name="controlling-a-sas-with-a-stored-access-policy"></a>Contrôle d’une SAP avec une stratégie d’accès stockée
Une signature d’accès partagé peut prendre deux formes :

* **SAS ad hoc :** lorsque vous créez un SAS ad hoc, l’heure de début hello, la durée d’expiration, et toutes les autorisations pour hello SAS sont spécifiées dans hello URI SAS (ou implicite, dans le cas de hello où l’heure de début est omise). Ce type de SAP peut être créé en tant que SAP de compte ou SAP de service.
* **Associations de sécurité avec la stratégie d’accès stockée :** une stratégie d’accès stockée est défini sur un conteneur de ressources--un conteneur d’objets blob, table, de file d’attente, ou partage--de fichiers et peut être utilisé toomanage les contraintes pour un ou plusieurs signatures d’accès partagé. Lorsque vous associez un SAS avec une stratégie d’accès stockée, hello SAS hérite des contraintes de hello--hello heure de début, heure d’expiration et autorisations--définies pour la stratégie d’accès stockée hello.

> [!NOTE]
> À l’heure actuelle, une SAP de compte doit être une SAP ad hoc. Les stratégies d’accès stockées ne sont pas encore prises en charge pour les SAP de compte.

Hello différence entre les formes hello deux est importante pour un scénario clé : la révocation. Comme un URI SAS est une URL, toute personne qui obtient hello SAS pouvez l’utiliser, quelle que soit la qui l’a créé. Si une SAP est publiée publiquement, il peut être utilisé par tout le monde dans Bonjour. Une SAP accorde l’accès tooresources tooanyone il possédant jusqu'à ce qu’un des quatre éléments se produit :

1. délai d’expiration Hello spécifié sur hello que SAS est atteinte.
2. délai d’expiration Hello spécifié sur la stratégie d’accès stockée hello référencée par hello que SAS est atteinte (si une stratégie d’accès stockée est référencée, et si elle spécifie un délai d’expiration). Cela peut se produire car hello est écoulé, ou vous avez modifié la stratégie d’accès stockée hello avec un délai d’expiration Bonjour passées, qui est une façon toorevoke hello SAS.
3. Hello stockés de la stratégie d’accès référencée par hello que SAS est supprimé, ce qui est hello de toorevoke une autre façon SAS. Notez que si vous recréez la stratégie d’accès stockée hello avec exactement de même nom, toutes les associations de sécurité existantes hello les jetons seront à nouveau des autorisations toohello conséquente valide associé cette stratégie d’accès stockée (en supposant que ce délai d’expiration hello sur hello SAP n’a pas été). Si vous prévoyez de toorevoke hello SAS, être vraiment toouse un nom différent si vous recréez la stratégie d’accès hello avec un délai d’expiration Bonjour futures.
4. Hello compte qui a été utilisé toocreate hello SAS est régénérée. La régénération d’une clé de compte entraîne tous les composants d’application à l’aide de ce tooauthenticate toofail clé jusqu'à ce qu’ils sont mis à jour toouse hello soit autre clé de compte valide ou une clé de compte qui vient d’être régénérée hello.

> [!IMPORTANT]
> Un URI de signature d’accès partagé est associé avec signature d’hello hello compte clé toocreate utilisés et hello stratégie d’accès stockée (le cas échéant). Si aucune stratégie d’accès stockée n’est spécifié, hello uniquement moyen toorevoke une signature d’accès partagé est clé de compte toochange hello.

## <a name="authenticating-from-a-client-application-with-a-sas"></a>Authentification à partir d’une application cliente avec la SAP
Un client qui est en possession d’une SAP peut utiliser hello SAS tooauthenticate une demande par rapport à un compte de stockage pour lesquels ils ne possèdent pas de clés de compte hello. Une SAP peut être incluse dans une chaîne de connexion, ou être utilisée directement à partir de méthode ou constructeur approprié de hello.

### <a name="using-a-sas-in-a-connection-string"></a>Utilisation d’une SAP dans une chaîne de connexion
[!INCLUDE [storage-use-sas-in-connection-string-include](../../../includes/storage-use-sas-in-connection-string-include.md)]

### <a name="using-a-sas-in-a-constructor-or-method"></a>Utilisation d’une SAP dans un constructeur ou une méthode
Plusieurs constructeurs de bibliothèque de client de stockage Azure et les surcharges de méthode offrent un paramètre SAS, afin que vous pouvez vous authentifier un service de toohello de demande avec une SAP.

Par exemple, un URI SAS est utilisé toocreate objet blob de blocs tooa référence. Hello SAS fournit hello seules informations d’identification nécessaires pour la demande de hello. référence blob de bloc Hello est ensuite utilisé pour une opération d’écriture :

```csharp
string sasUri = "https://storagesample.blob.core.windows.net/sample-container/" +
    "sampleBlob.txt?sv=2015-07-08&sr=b&sig=39Up9JzHkxhUIhFEjEH9594DJxe7w6cIRCg0V6lCGSo%3D" +
    "&se=2016-10-18T21%3A51%3A37Z&sp=rcw";

CloudBlockBlob blob = new CloudBlockBlob(new Uri(sasUri));

// Create operation: Upload a blob with hello specified name toohello container.
// If hello blob does not exist, it will be created. If it does exist, it will be overwritten.
try
{
    MemoryStream msWrite = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
    msWrite.Position = 0;
    using (msWrite)
    {
        await blob.UploadFromStreamAsync(msWrite);
    }

    Console.WriteLine("Create operation succeeded for SAS {0}", sasUri);
    Console.WriteLine();
}
catch (StorageException e)
{
    if (e.RequestInformation.HttpStatusCode == 403)
    {
        Console.WriteLine("Create operation failed for SAS {0}", sasUri);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
    else
    {
        Console.WriteLine(e.Message);
        Console.ReadLine();
        throw;
    }
}

```

## <a name="best-practices-when-using-sas"></a>Bonnes pratiques lors de l’utilisation de SAP
Lorsque vous utilisez des signatures d’accès partagé dans vos applications, vous devez toobe conscient des risques potentiels deux :

* Si une signature d'accès partagé est divulguée, toute personne qui se la procure peut s'en servir et votre compte de stockage court donc le risque d'être compromis.
* Si un SAS fourni tooa client application expire et l’application hello est impossible de tooretrieve une nouvelle SAP à partir de votre service, des fonctionnalités de l’application hello peuvent être entravée.

Hello les recommandations suivantes pour l’utilisation de signatures d’accès partagé peuvent aider à réduire ces risques :

1. **Toujours utiliser HTTPS** toocreate ou distribuer un SAS. Si une SAP est transmise via HTTP et interceptée, un attaquant lors d’une attaque de man-in-the-middle est en mesure de tooread hello SAS et l’utiliser comme hello destiné utilisateur peut avoir compromettre des données sensibles ou permettant la corruption des données hello utilisateur malveillant.
2. **Référencez si possible les stratégies d'accès stockées.** Stockées permettent de stratégies d’accès hello d’autorisations de toorevoke option sans avoir des clés de compte de stockage tooregenerate hello. Définir l’expiration de hello très bien dans hello future (ou infinie) et vérifiez qu’il est régulièrement mis à jour les toomove plus loin dans hello futures.
3. **Utilisez des heures d'expiration avec une échéance à court terme sur une signature d'accès partagé ad hoc.** De cette manière, même si une signature d’accès partagé est compromise, elle n’est valide que pendant une courte durée. Cette pratique est particulièrement importante si vous ne pouvez pas référencer une stratégie d'accès stockée. Les délais d’expiration court terme également limitent hello de données qui peuvent être écrites tooa blob en limitant hello temps disponible tooupload tooit.
4. **Disposer de clients renouveler automatiquement hello SAS si nécessaire.** Les clients doivent renouveler hello SAS bien avant l’expiration de hello, dans le temps de tooallow d’ordre des nouvelles tentatives si le service hello fournissant hello SAS n’est pas disponible. Si votre SAS doit toobe utilisé pour un petit nombre d’exécution, les opérations de courte durée de vie sont attendu toobe effectué dans la période d’expiration de hello, puis peut-être inutile hello que SAS n’est pas normalement toobe renouvelé. Toutefois, si vous avez client qui envoie régulièrement des requêtes via SAS, possibilité de hello d’expiration entre en jeu. Hello essentiel est toobalance hello nécessaire pour hello SAS toobe courte durée de vie (comme indiqué plus haut) avec tooensure besoin hello qui hello client demande le renouvellement tôt suffisamment (tooavoid interruption de service en raison de renouvellement de toosuccessful préalable toohello SAS qui arrive à expiration).
5. **Faites attention à la date de début de la signature d’accès partagé.** Si vous définissez l’heure de début hello pour une SAP trop**maintenant**, puis en raison du décalage tooclock (différences dans le temps actuel en fonction de machines de toodifferent), échecs peuvent être observés par intermittence pour hello premières minutes. En général, définir toobe de temps de démarrage hello au moins 15 minutes Bonjour passées. ou ne la définissez pas du tout, et elle sera alors valide immédiatement dans tous les cas. Hello même tooexpiry temps--s’applique généralement, n’oubliez pas que vous pouvez observer des minutes too15 d’horloge décalage dans les deux sens sur demande. Pour les clients à l’aide de REST version antérieure too2012-02-12, hello de durée maximale pour un SAS qui ne fait pas référence à une stratégie d’accès stockée est de 1 heure et les stratégies de spécification à long terme que qui échoue.
6. **Être spécifique hello ressource toobe est accédé.** Meilleure pratique de sécurité est tooprovide un utilisateur avec des privilèges requis minimaux hello. Si un utilisateur a seulement besoin d’un accès en lecture tooa seule entité, puis accordez-leur les toothat des accès en lecture seule entité et l’accès en lecture/écriture/suppression pas tooall entités. Cela vous permet également de réduire les dommages hello si une SAP est compromise, car hello SAS a moins de puissance entre les mains d’une personne malveillante hello.
7. **Sachez que toute utilisation de votre compte sera facturée, y compris pour les signatures d'accès partagé.** Si vous fournissez un accès en écriture tooa blob, un utilisateur peut choisir un blob de 200 Go tooupload. Si vous leur avez donné accès en lecture ainsi, ils peuvent choisir toodownload 10 fois, souscrivant 2 To en sortie le coût pour vous. Là encore, fournir des autorisations limitées toohelp limiter les actions des utilisateurs malveillants d’hello. Utilisez éphémères SAS tooreduce cette menace (mais penser horloge inclinaison sur l’heure de fin hello).
8. **Validez les données écrites avec une signature d'accès partagé.** Lorsqu’une application cliente écrit le compte de stockage de données tooyour, gardez à l’esprit qu’il peut y avoir des problèmes avec ces données. Si votre application nécessite que les données être validées ou autorisées avant qu’il soit prêt toouse, vous devez effectuer cette validation une fois les données de salutation sont écrit et avant d’être utilisée par votre application. Cette pratique protège également contre les données endommagées ou malveillantes écrites tooyour compte, soit par un utilisateur qui correctement acquis hello SAP, soit par un utilisateur d’exploiter une fuite SAP.
9. **N'utilisez pas toujours une signature d'accès partagé.** Parfois, les risques de hello associés à une opération particulière par rapport à votre compte de stockage dépassent les avantages de hello de SAP. Pour ces opérations, créer un service de couche intermédiaire qui écrit le compte de stockage tooyour après avoir effectué l’entreprise la règle de validation, l’authentification et l’audit. En outre, il est parfois plus simple accès toomanage par d’autres moyens. Par exemple, si vous souhaitez toomake tous les objets BLOB dans un conteneur accessibles publiquement en lecture, vous pouvez apporter hello conteneur Public, habituellement, un client de tooevery SAS pour l’accès.
10. **Utilisez stockage Analytique toomonitor votre application.** Vous pouvez utiliser la journalisation et tooobserve métriques une surutilisation échecs d’authentification en raison de la panne tooan votre SAS fournisseur service ou toohello par inadvertance la suppression d’une stratégie d’accès stockée. Consultez hello [Blog de l’équipe stockage Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx) pour plus d’informations.

## <a name="sas-examples"></a>Exemples de SAP
Vous trouverez ci-dessous des exemples des deux types de signatures d’accès partagé, SAP de compte et SAP de service.

toorun ces exemples c#, vous devez hello tooreference suivant les packages NuGet dans votre projet :

* [Bibliothèque de Client de stockage Azure pour .NET](http://www.nuget.org/packages/WindowsAzure.Storage), version 6.x ou version ultérieure (compte toouse SAS).
* [Gestionnaire de configuration Azure](http://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager)

Pour obtenir des exemples supplémentaires qui montrent comment toocreate et test d’une SAS, consultez [Azure des exemples de Code pour le stockage](https://azure.microsoft.com/documentation/samples/?service=storage).

### <a name="example-create-and-use-an-account-sas"></a>Exemple : création et utilisation d’une SAP de compte
Hello exemple de code suivant crée un compte d’associations de sécurité sont valides pour hello Blob et les services de fichiers, et donne hello client les autorisations de lecture, écriture et liste tooaccess au niveau du service API. le compte Hello SAS restreint hello protocole tooHTTPS, afin de la demande de hello doit être effectuée à l’aide de HTTPS.

```csharp
static string GetAccountSASToken()
{
    // toocreate hello account SAS, you need toouse your shared key credentials. Modify for your account.
    const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

    // Create a new access policy for hello account.
    SharedAccessAccountPolicy policy = new SharedAccessAccountPolicy()
        {
            Permissions = SharedAccessAccountPermissions.Read | SharedAccessAccountPermissions.Write | SharedAccessAccountPermissions.List,
            Services = SharedAccessAccountServices.Blob | SharedAccessAccountServices.File,
            ResourceTypes = SharedAccessAccountResourceTypes.Service,
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Protocols = SharedAccessProtocol.HttpsOnly
        };

    // Return hello SAS token.
    return storageAccount.GetSharedAccessSignature(policy);
}
```

toouse hello compte SAP tooaccess niveau de service API pour le service d’objets Blob hello, construire un objet Blob client hello SAS et hello du point de terminaison de stockage Blob pour votre compte de stockage.

```csharp
static void UseAccountSAS(string sasToken)
{
    // Create new storage credentials using hello SAS token.
    StorageCredentials accountSAS = new StorageCredentials(sasToken);
    // Use these credentials and hello account name toocreate a Blob service client.
    CloudStorageAccount accountWithSAS = new CloudStorageAccount(accountSAS, "account-name", endpointSuffix: null, useHttps: true);
    CloudBlobClient blobClientWithSAS = accountWithSAS.CreateCloudBlobClient();

    // Now set hello service properties for hello Blob client created with hello SAS.
    blobClientWithSAS.SetServiceProperties(new ServiceProperties()
    {
        HourMetrics = new MetricsProperties()
        {
            MetricsLevel = MetricsLevel.ServiceAndApi,
            RetentionDays = 7,
            Version = "1.0"
        },
        MinuteMetrics = new MetricsProperties()
        {
            MetricsLevel = MetricsLevel.ServiceAndApi,
            RetentionDays = 7,
            Version = "1.0"
        },
        Logging = new LoggingProperties()
        {
            LoggingOperations = LoggingOperations.All,
            RetentionDays = 14,
            Version = "1.0"
        }
    });

    // hello permissions granted by hello account SAS also permit you tooretrieve service properties.
    ServiceProperties serviceProperties = blobClientWithSAS.GetServiceProperties();
    Console.WriteLine(serviceProperties.HourMetrics.MetricsLevel);
    Console.WriteLine(serviceProperties.HourMetrics.RetentionDays);
    Console.WriteLine(serviceProperties.HourMetrics.Version);
}
```

### <a name="example-create-a-stored-access-policy"></a>Exemple : création d’une stratégie d’accès stockée
Hello de code suivant crée une stratégie d’accès stockée sur un conteneur. Vous pouvez utiliser des contraintes de toospecify hello accès stratégie pour un service SAS sur le conteneur de hello ou ses objets BLOB.

```csharp
private static async Task CreateSharedAccessPolicyAsync(CloudBlobContainer container, string policyName)
{
    // Create a new shared access policy and define its constraints.
    // hello access policy provides create, write, read, list, and delete permissions.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
        // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
        SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.List |
            SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Create | SharedAccessBlobPermissions.Delete
    };

    // Get hello container's existing permissions.
    BlobContainerPermissions permissions = await container.GetPermissionsAsync();

    // Add hello new policy toohello container's permissions, and set hello container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    await container.SetPermissionsAsync(permissions);
}
```

### <a name="example-create-a-service-sas-on-a-container"></a>Exemple : création d’une SAP de service sur un conteneur
Hello suivante de code crée une SAP sur un conteneur. Si le nom hello d’une stratégie d’accès stockée existante est fourni, cette stratégie est associée à hello SAS. Si aucune stratégie d’accès stockée n’est fourni, code de hello crée ensuite un SAS ad hoc sur le conteneur de hello.

```csharp
private static string GetContainerSasUri(CloudBlobContainer container, string storedPolicyName = null)
{
    string sasContainerToken;

    // If no stored policy is specified, create a new access policy and define its constraints.
    if (storedPolicyName == null)
    {
        // Note that hello SharedAccessBlobPolicy class is used both toodefine hello parameters of an ad-hoc SAS, and
        // tooconstruct a shared access policy that is saved toohello container's shared access policies.
        SharedAccessBlobPolicy adHocPolicy = new SharedAccessBlobPolicy()
        {
            // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
            // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List
        };

        // Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
        sasContainerToken = container.GetSharedAccessSignature(adHocPolicy, null);

        Console.WriteLine("SAS for blob container (ad hoc): {0}", sasContainerToken);
        Console.WriteLine();
    }
    else
    {
        // Generate hello shared access signature on hello container. In this case, all of hello constraints for the
        // shared access signature are specified on hello stored access policy, which is provided by name.
        // It is also possible toospecify some constraints on an ad-hoc SAS and others on hello stored access policy.
        sasContainerToken = container.GetSharedAccessSignature(null, storedPolicyName);

        Console.WriteLine("SAS for blob container (stored access policy): {0}", sasContainerToken);
        Console.WriteLine();
    }

    // Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

### <a name="example-create-a-service-sas-on-a-blob"></a>Exemple : création d’une SAP de service sur un objet blob
Hello suivante de code crée une SAP sur un objet blob. Si le nom hello d’une stratégie d’accès stockée existante est fourni, cette stratégie est associée à hello SAS. Si aucune stratégie d’accès stockée n’est fourni, code de hello crée ensuite un SAS ad hoc sur l’objet blob de hello.

```csharp
private static string GetBlobSasUri(CloudBlobContainer container, string blobName, string policyName = null)
{
    string sasBlobToken;

    // Get a reference tooa blob within hello container.
    // Note that hello blob may not exist yet, but a SAS can still be created for it.
    CloudBlockBlob blob = container.GetBlockBlobReference(blobName);

    if (policyName == null)
    {
        // Create a new access policy and define its constraints.
        // Note that hello SharedAccessBlobPolicy class is used both toodefine hello parameters of an ad-hoc SAS, and
        // tooconstruct a shared access policy that is saved toohello container's shared access policies.
        SharedAccessBlobPolicy adHocSAS = new SharedAccessBlobPolicy()
        {
            // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
            // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Create
        };

        // Generate hello shared access signature on hello blob, setting hello constraints directly on hello signature.
        sasBlobToken = blob.GetSharedAccessSignature(adHocSAS);

        Console.WriteLine("SAS for blob (ad hoc): {0}", sasBlobToken);
        Console.WriteLine();
    }
    else
    {
        // Generate hello shared access signature on hello blob. In this case, all of hello constraints for the
        // shared access signature are specified on hello container's stored access policy.
        sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

        Console.WriteLine("SAS for blob (stored access policy): {0}", sasBlobToken);
        Console.WriteLine();
    }

    // Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

## <a name="conclusion"></a>Conclusion
Signatures d’accès partagé sont utiles pour fournir des autorisations limitées tooclients de compte de stockage tooyour qui ne devrait pas de clé de compte hello. Par conséquent, ils sont une partie essentielle hello du modèle de sécurité pour les applications qui utilisent le stockage Azure. Si vous suivez les recommandations hello répertoriées ici, vous pouvez utiliser SAS tooprovide une plus grande souplesse de tooresources d’accès dans votre compte de stockage, sans compromettre la sécurité hello de votre application.

## <a name="next-steps"></a>Étapes suivantes
* [Gérer les objets BLOB et l’accès en lecture anonyme toocontainers](../blobs/storage-manage-access-to-resources.md)
* [Délégation de l'accès avec une signature d'accès partagé](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [Présentation des signatures d’accès partagé de table et de file d’attente](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)
