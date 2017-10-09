---
title: "l’authentification de Service Bus aaaAzure avec des Signatures d’accès partagé | Documents Microsoft"
description: "Vue d’ensemble de l’authentification de Service Bus à l’aide des signatures d’accès partagé, plus d’informations sur l’authentification SAP avec Azure Service Bus."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: 773bb11720384d7245820b56dc25b8e064ffa746
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-authentication-with-shared-access-signatures"></a>Authentification de Service Bus avec les signatures d’accès partagé

*Signatures d’accès partagé* (SAP) est hello principal mécanisme de sécurité pour la messagerie Service Bus. Cet article traite de SAS, comment ils fonctionnent et comment toouse dans un moyen indépendant de la plateforme.

L’authentification SAP permet des applications tooauthenticate tooService Bus à l’aide d’une clé d’accès configurée sur l’espace de noms hello, ou sur hello messagerie entité (file d’attente ou rubrique) avec les droits spécifiques sont associés. Vous pouvez ensuite utiliser cette clé toogenerate un jeton SAP que les clients peuvent utiliser ensuite tooauthenticate tooService Bus.

L’authentification SAP est inclus dans hello Azure SDK version 2.0 et versions ultérieure.

## <a name="overview-of-sas"></a>Présentation des signatures d’accès partagé (SAS)

Les signatures d’accès partagé sont un mécanisme d’authentification basé sur des hachages sécurisés SHA-256 ou des URI. Les signatures d’accès partagé sont un mécanisme extrêmement puissant qui est utilisé par tous les services Service Bus. En fait, les SAP ont deux composants : une *stratégie d’accès partagé* et une *signature d’accès partagé* (souvent appelée *jeton*).

L’authentification SAP dans le Bus de Service implique une configuration de hello d’une clé de chiffrement avec les droits correspondants sur une ressource de Service Bus. Les clients revendication accès tooService Bus ressources à l’aide d’un jeton SAP. Ce jeton se compose de l’URI en cours d’accès de la ressource hello et un délai d’expiration signé avec hello configuré la clé.

Vous pouvez configurer des règles d’autorisation de signature d’accès partagé sur des [relais](service-bus-fundamentals-hybrid-solutions.md#relays), des [files d’attente](service-bus-fundamentals-hybrid-solutions.md#queues) et des [rubriques](service-bus-fundamentals-hybrid-solutions.md#topics) Service Bus.

L’authentification SAP utilise hello suivant d’éléments :

* [Règle d’autorisation d’accès partagée](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) : clé de chiffrement principale cryptée en Base64 à 256 bits, une clé secondaire facultative et un nom de clé et des droits associés (une collection de droits *écouter*, *envoyer* ou *gérer*).
* [Signature d’accès partagé](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider) jeton : généré à l’aide de hello HMAC-SHA256 d’une chaîne de ressource, consistant à hello URI de ressource hello qui est accessible et d’expiration, avec la clé de chiffrement hello. signature de Hello et autres éléments décrits dans les sections suivantes de hello sont mis en forme dans un Bonjour de tooform chaîne jeton SAP.

## <a name="shared-access-policy"></a>Stratégie d’accès partagé

Un toounderstand plus important sur les associations de sécurité est qu’elle démarre avec une stratégie. Pour chaque stratégie, vous choisissez trois éléments d’information : le **nom**, l’**étendue** et les **autorisations**. Hello **nom** est simplement que ; un nom unique dans cette étendue. Hello étendue est assez facile : hello son URI de ressource hello en question. Pour un espace de noms Service Bus, hello porte le nom de domaine complet hello (FQDN), tel que `https://<yournamespace>.servicebus.windows.net/`.

les autorisations disponibles Hello pour une stratégie sont en grande partie explicites :

* Envoyer
* Écouter
* Gérer

Après avoir créé la stratégie de hello, il est attribué un *clé primaire* et un *clé secondaire*. Il s’agit de clés de chiffrement fortes. Ne pas perdre les ou les fuites - ils soient toujours disponibles dans hello [portail Azure][Azure portal]. Vous pouvez utiliser une des clés de hello généré, et vous pouvez les régénérer à tout moment. Toutefois, si vous régénérez ou modifiez la clé primaire de hello dans la stratégie de hello, toutes les Signatures d’accès partagé créé à partir de celui-ci sont invalidés.

Lorsque vous créez un espace de noms Service Bus, une stratégie est automatiquement créée pour l’espace de noms complet hello appelé **RootManageSharedAccessKey**, et cette stratégie a toutes les autorisations. Étant donné que vous ne vous connectez pas en tant que **racine**, n’utilisez cette stratégie que si vous avez une très bonne raison de le faire. Vous pouvez créer des stratégies supplémentaires Bonjour **configurer** onglet de l’espace de noms hello dans le portail de hello. Il est important toonote qui a un niveau d’arborescence unique dans Service Bus (espace de noms, file d’attente, etc.) peut uniquement avoir des too12 stratégies jointes tooit.

## <a name="configuration-for-shared-access-signature-authentication"></a>Configuration de l’authentification de signature d’accès partagé
Vous pouvez configurer hello [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) règle sur les espaces de noms Service Bus, les files d’attente ou rubriques. Configuration d’un [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) sur un Bus de Service d’abonnement est actuellement pas pris en charge, mais vous pouvez utiliser les règles configurées sur une toosubscriptions d’accès toosecure espace de noms ou une rubrique. Pour obtenir un exemple fonctionnel qui illustre cette procédure, consultez hello [l’authentification à l’aide de l’accès Signature partagé (SAS) avec les abonnements Service Bus](http://code.msdn.microsoft.com/Using-Shared-Access-e605b37c) exemple.

Un maximum de 12 règles de ce type peut être configuré sur un espace de noms, une file d’attente ou une rubrique Service Bus. Les règles qui sont configurés sur un espace de noms Service Bus s’appliquent tooall des entités dans cet espace de noms.

![SAS](./media/service-bus-sas/service-bus-namespace.png)

Dans cette figure, hello *manageRuleNS*, *sendRuleNS*, et *listenRuleNS* les règles d’autorisation s’appliquent à la file d’attente de tooboth Q1 et rubrique T1, tandis que *listenRuleQ*  et *sendRuleQ* s’appliquent uniquement tooqueue Q1 et *sendRuleT* s’applique uniquement tootopic T1.

Hello principaux paramètres d’un [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) sont les suivantes :

| Paramètre | Description |
| --- | --- |
| *Nom de clé* |Chaîne qui décrit la règle d’autorisation hello. |
| *Clé primaire* |Une codée en base64 256 bits clé primaire pour signer et valider un jeton SAS hello. |
| *Clé secondaire* |Une codée en base64 256 bits clé secondaire pour signer et valider un jeton SAS hello. |
| *Droits d’accès* |Liste des droits d’accès accordées par la règle d’autorisation hello. Ces droits peuvent être n’importe quel ensemble contenant les droits d’écoute, d’envoi et de gestion. |

Lorsqu’un espace de noms Service Bus est configuré, un [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule), avec [KeyName](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_KeyName) défini trop**RootManageSharedAccessKey**, est créé par défaut.

## <a name="generate-a-shared-access-signature-token"></a>Création d’une signature d’accès partagé (jeton)

stratégie Hello proprement dite n’est pas jeton d’accès hello pour Service Bus. Il s’agit d’objet hello à partir de quels hello jeton d’accès est généré - à l’aide de la clé primaire ou secondaire hello. Tout client qui a toohello d’accès spécifiés dans la règle de l’autorisation d’accès partagé hello des clés de signature peut générer un jeton SAS hello. jeton de Hello est généré en soigneusement en créant une chaîne Bonjour suivant le format :

```
SharedAccessSignature sig=<signature-string>&se=<expiry>&skn=<keyName>&sr=<URL-encoded-resourceURI>
```

Où `signature-string` est étendue hello du jeton de hello hachage hello SHA-256 (**étendue** comme décrit dans la section précédente de hello) avec un CRLF ajouté et un délai d’expiration (en secondes depuis l’époque de hello : `00:00:00 UTC` 1er janvier 1970). 

> [!NOTE]
> tooavoid une heure d’expiration du jeton court, il est recommandé que vous codez une durée d’expiration de hello en tant qu’au moins un entier non signé 32 bits, ou, de préférence un entier long (64 bits).  
> 
> 

hachage de Hello semble similaire toohello suivant pseudo-code et retourne 32 octets.

```
SHA-256('https://<yournamespace>.servicebus.windows.net/'+'\n'+ 1438205742)
```

les valeurs non hachées Hello sont Bonjour **SharedAccessSignature** afin que hello destinataire peut calculer hello hachage de chaîne hello avec les mêmes paramètres, toobe sûr qu’il retourne hello même résultat. Hello URI Spécifie l’étendue de hello et nom de la clé hello identifie le hachage hello toocompute hello stratégie toobe utilisé. Ceci est important du point de vue de la sécurité. Si la signature de hello ne correspond pas au destinataire hello (Service Bus) calcule, l’accès est refusé. À ce stade, vous pouvez être que cet expéditeur hello avait la clé d’accès toohello et doit disposer des autorisations hello spécifiées dans la stratégie de hello.

Notez que vous devez utiliser l’URI de ressource hello codée pour cette opération. URI de ressource Hello est hello QU'URI complet de hello toowhich accès aux ressources de Service Bus est revendiqué. Par exemple, `http://<namespace>.servicebus.windows.net/<entityPath>` ou `sb://<namespace>.servicebus.windows.net/<entityPath>` ; qui est, `http://contoso.servicebus.windows.net/contosoTopics/T1/Subscriptions/S3`.

règle d’autorisation de Hello accès partagé utilisé pour la signature doit être configuré sur l’entité hello spécifiée par cet URI, ou par un de ses parents hiérarchiques. Par exemple, `http://contoso.servicebus.windows.net/contosoTopics/T1` ou `http://contoso.servicebus.windows.net` dans l’exemple précédent de hello.

Un jeton SAP est valable pour toutes les ressources sous hello `<resourceURI>` utilisé Bonjour `signature-string`.

Hello [KeyName](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_KeyName) Bonjour SAS jeton fait référence toohello **keyName** Hello règle d’autorisation d’accès partagé utilisé le jeton de hello toogenerate.

Hello *URL-encoded-resourceURI* doit être identique à celle de l’URI utilisé dans la chaîne de signature hello lors du calcul de hello de signature de hello de hello hello. Elle doit être [encodée en pourcentage](https://msdn.microsoft.com/library/4fkewx0t.aspx).

Il est recommandé de régénérer régulièrement les clés de hello utilisées dans hello [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) objet. Les applications doivent utiliser généralement hello [PrimaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_PrimaryKey) toogenerate un jeton SAP. Lors de la régénération des clés de hello, vous devez remplacer hello [SecondaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_SecondaryKey) avec l’ancien serveur principal de hello de clé et générer une nouvelle clé en tant que clé primaire hello. Cela vous permet de toocontinue à l’aide des jetons d’autorisation qui ont été émis avec une clé primaire de hello ancien, et qui n’ont pas encore expiré.

Si une clé est compromise et que vous avez toorevoke hello clés, vous pouvez régénérer les deux hello [PrimaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_PrimaryKey) et hello [SecondaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_SecondaryKey) d’un [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule), en les remplaçant avec de nouvelles clés. Cette procédure annule tous les jetons signés avec les anciennes clés de hello.

## <a name="how-toouse-shared-access-signature-authentication-with-service-bus"></a>Comment toouse l’authentification de Signature d’accès partagé avec Service Bus

Hello les scénarios suivants inclure la configuration des règles d’autorisation, de la génération de jetons SAP et l’autorisation du client.

Pour un complet exemple fonctionnel d’une application de Service Bus qui illustre hello configuration et l’autorisation SAP, consultez [l’authentification de Signature d’accès partagé avec Service Bus](http://code.msdn.microsoft.com/Shared-Access-Signature-0a88adf8). Un exemple qui montre comment utiliser les règles de d’autorisation SAP configurées sur les espaces de noms ou des rubriques d’abonnements de Service Bus toosecure hello est disponible ici : [l’authentification à l’aide de l’accès Signature partagé (SAS) avec les abonnements Service Bus ](http://code.msdn.microsoft.com/Using-Shared-Access-e605b37c).

## <a name="access-shared-access-authorization-rules-on-a-namespace"></a>Accès aux règles d’autorisation d’accès partagé sur un espace des noms

Opérations sur la racine d’espace de noms hello Bus de Service requièrent l’authentification par certificat. Vous devez charger un certificat de gestion pour votre abonnement Azure. tooupload un certificat de gestion, suivez les étapes de hello [ici](../cloud-services/cloud-services-configure-ssl-certificate-portal.md#step-3-upload-a-certificate), à l’aide de hello [portail Azure][Azure portal]. Pour plus d’informations sur les certificats de gestion Azure, consultez hello [vue d’ensemble de certificats Azure](../cloud-services/cloud-services-certs-create.md#what-are-management-certificates).

point de terminaison Hello pour accéder aux règles de d’autorisation d’accès partagé sur un espace de noms Service Bus est la suivante :

```http
https://management.core.windows.net/{subscriptionId}/services/ServiceBus/namespaces/{namespace}/AuthorizationRules/
```

toocreate un [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) objet sur un espace de noms Service Bus, exécuter une opération POST sur ce point de terminaison avec les informations de règle hello sérialisées en tant que JSON ou XML. Par exemple :

```csharp
// Base address for accessing authorization rules on a namespace
string baseAddress = @"https://management.core.windows.net/<subscriptionId>/services/ServiceBus/namespaces/<namespace>/AuthorizationRules/";

// Configure authorization rule with base64-encoded 256-bit key and Send rights
var sendRule = new SharedAccessAuthorizationRule("contosoSendAll",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Send });

// Operations on hello Service Bus namespace root require certificate authentication.
WebRequestHandler handler = new WebRequestHandler
{
    ClientCertificateOptions = ClientCertificateOption.Manual
};
// Access hello management certificate by subject name
handler.ClientCertificates.Add(GetCertificate(<certificateSN>));

HttpClient httpClient = new HttpClient(handler)
{
    BaseAddress = new Uri(baseAddress)
};
httpClient.DefaultRequestHeaders.Accept.Add(
    new MediaTypeWithQualityHeaderValue("application/json"));
httpClient.DefaultRequestHeaders.Add("x-ms-version", "2015-01-01");

// Execute a POST operation on hello baseAddress above toocreate an auth rule
var postResult = httpClient.PostAsJsonAsync("", sendRule).Result;
```

De même, utilisez une opération GET sur les règles d’autorisation hello point de terminaison tooread hello configuré sur l’espace de noms hello.

tooupdate ou supprimer une règle d’autorisation spécifique, utilisez hello après le point de terminaison :

```http
https://management.core.windows.net/{subscriptionId}/services/ServiceBus/namespaces/{namespace}/AuthorizationRules/{KeyName}
```

## <a name="access-shared-access-authorization-rules-on-an-entity"></a>Accès aux règles d’autorisation d’accès partagé sur une entité

Vous pouvez accéder à un [Microsoft.ServiceBus.Messaging.SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) objet configuré sur une file d’attente du Bus de Service ou une rubrique via hello [AuthorizationRules](/dotnet/api/microsoft.servicebus.messaging.authorizationrules) collection Bonjour correspondant [QueueDescription](/dotnet/api/microsoft.servicebus.messaging.queuedescription) ou [TopicDescription](/dotnet/api/microsoft.servicebus.messaging.topicdescription).

Hello suivant de code montre le fonctionnement des règles de l’autorisation de tooadd pour une file d’attente.

```csharp
// Create an instance of NamespaceManager for hello operation
NamespaceManager nsm = NamespaceManager.CreateFromConnectionString(
    <connectionString> );
QueueDescription qd = new QueueDescription( <qPath> );

// Create a rule with send rights with keyName as "contosoQSendKey"
// and add it toohello queue description.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoSendKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Send }));

// Create a rule with listen rights with keyName as "contosoQListenKey"
// and add it toohello queue description.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoQListenKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Listen }));

// Create a rule with manage rights with keyName as "contosoQManageKey"
// and add it toohello queue description.
// A rule with manage rights must also have send and receive rights.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoQManageKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] {AccessRights.Manage, AccessRights.Listen, AccessRights.Send }));

// Create hello queue.
nsm.CreateQueue(qd);
```

## <a name="use-shared-access-signature-authorization"></a>Utilisation de l’autorisation de la signature d’accès partagé (SAP)

Les applications à l’aide de hello Azure .NET SDK avec les bibliothèques .NET Service Bus hello peuvent utiliser une autorisation SAP via hello [SharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider) classe. Hello de code suivant illustre utilisation hello de file d’attente hello fournisseur de jetons toosend messages tooa Service Bus.

```csharp
Uri runtimeUri = ServiceBusEnvironment.CreateServiceUri("sb",
    <yourServiceNamespace>, string.Empty);
MessagingFactory mf = MessagingFactory.Create(runtimeUri,
    TokenProvider.CreateSharedAccessSignatureTokenProvider(keyName, key));
QueueClient sendClient = mf.CreateQueueClient(qPath);

//Sending hello message tooqueue.
BrokeredMessage helloMessage = new BrokeredMessage("Hello, Service Bus!");
helloMessage.MessageId = "SAS-Sample-Message";
sendClient.Send(helloMessage);
```

Les applications peuvent également utiliser des associations de sécurité pour l’authentification en utilisant une chaîne de connexion dans les méthodes qui acceptent des chaînes de connexion.

Notez que toouse une autorisation SAP avec relais Service Bus, vous pouvez utiliser des clés SAP configurées sur l’espace de noms Service Bus hello. Si vous créez explicitement un relais sur l’espace de noms hello ([NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) avec un [RelayDescription](/dotnet/api/microsoft.servicebus.messaging.relaydescription)) de l’objet, vous pouvez définir des règles de SAP hello pour ce relais. toouse une autorisation SAP avec les abonnements Service Bus, vous pouvez utiliser des clés SAP configurées sur un espace de noms Service Bus ou sur une rubrique.

## <a name="use-hello-shared-access-signature-at-http-level"></a>Utilisez hello Signature d’accès partagé (au niveau HTTP)

Maintenant que vous savez comment toocreate Signatures d’accès partagé pour toutes les entités de Service Bus, vous êtes prêt à tooperform une requête HTTP POST :

```http
POST https://<yournamespace>.servicebus.windows.net/<yourentity>/messages
Content-Type: application/json
Authorization: SharedAccessSignature sr=https%3A%2F%2F<yournamespace>.servicebus.windows.net%2F<yourentity>&sig=<yoursignature from code above>&se=1438205742&skn=KeyName
ContentType: application/atom+xml;type=entry;charset=utf-8
``` 

N’oubliez pas que cela fonctionne pour tout. Vous pouvez créer une signature d’accès partagé pour une file d’attente, une rubrique ou un abonnement. 

Si vous donnez à un expéditeur ou un client un jeton SAP, ils n’ont pas la clé de hello directement, et ils ne peuvent pas inverser hello hachage tooobtain il. Ainsi, vous contrôlez le contenu auquel il peut accéder et pour quelle durée. Un tooremember point essentiel est que si vous modifiez la clé primaire de hello dans la stratégie de hello, toutes les Signatures d’accès partagé créé à partir de celui-ci sera invalidés.

## <a name="use-hello-shared-access-signature-at-amqp-level"></a>Utilisez hello Signature d’accès partagé (au niveau AMQP)

Dans la section précédente de hello, vous avez vu comment toouse hello jeton SAS avec une requête HTTP POST pour envoyer des données toohello Service Bus. Comme vous le savez, vous pouvez accéder à des Bus de Service à l’aide de hello avancé protocole AMQP (Message Queuing) qui est toouse de protocole hello préféré pour des raisons de performances, dans de nombreux scénarios. Hello d’utilisation de jeton SAS avec AMQP est décrite dans le document de hello [AMQP Claim-Based sécurité Version 1.0](https://www.oasis-open.org/committees/download.php/50506/amqp-cbs-v1%200-wd02%202013-08-12.doc) qui est en brouillon de travail depuis 2013, mais il est bien pris en charge par Azure aujourd'hui.

Avant de commencer toosend données tooService Bus, serveur de publication hello doit envoyer un jeton SAS hello à l’intérieur d’un AMQP message tooa bien défini AMQP nœud nommé **$cbs** (vous pouvez voir « spécial » file d’attente utilisée par hello service tooacquire et valider l’ensemble jetons SAP Hello). serveur de publication Hello doit spécifier hello **ReplyTo** champ à l’intérieur du message AMQP hello ; il s’agit de nœud hello dans le hello service répond toohello le serveur de publication avec un résultat de validation du jeton (un modèle de demande/réponse simple entre hello hello serveur de publication et de service). Création de ce nœud de la réponse « volée hello, « parler de « création dynamique de nœud distant » comme décrit dans la spécification de hello AMQP 1.0. Après avoir vérifié le que jeton SAS hello est valid, serveur de publication hello peut avancer et démarrer le service de toohello toosend données.

Hello étapes suivantes montrent comment toosend hello jeton SAS avec le protocole AMQP à l’aide de hello [AMQP.Net Lite](https://github.com/Azure/amqpnetlite) bibliothèque. Cela est utile si vous ne pouvez pas utiliser officielle de hello SDK du Bus de Service (par exemple sur WinRT, .net Compact Framework, le .net Framework de Micro et Mono) développement en C\#. Bien entendu, cette bibliothèque est utile toohelp comprendre la sécurité basée sur les revendications fonctionne au niveau AMQP de hello, comme vous l’avez vu comment il fonctionne au niveau de hello HTTP (avec un HTTP POST demande et hello SAS jeton hello envoyé à l’intérieur d’en-tête « Authorization »). Si vous n’avez pas besoin ces connaissances approfondies sur AMQP, vous pouvez utiliser officielle de hello SDK du Bus de Service avec .net applications Framework, qui fera pour vous.

### <a name="c35"></a>C&#35;

```csharp
/// <summary>
/// Send claim-based security (CBS) token
/// </summary>
/// <param name="shareAccessSignature">Shared access signature (token) toosend</param>
private bool PutCbsToken(Connection connection, string sasToken)
{
    bool result = true;
    Session session = new Session(connection);

    string cbsClientAddress = "cbs-client-reply-to";
    var cbsSender = new SenderLink(session, "cbs-sender", "$cbs");
    var cbsReceiver = new ReceiverLink(session, cbsClientAddress, "$cbs");

    // construct hello put-token message
    var request = new Message(sasToken);
    request.Properties = new Properties();
    request.Properties.MessageId = Guid.NewGuid().ToString();
    request.Properties.ReplyTo = cbsClientAddress;
    request.ApplicationProperties = new ApplicationProperties();
    request.ApplicationProperties["operation"] = "put-token";
    request.ApplicationProperties["type"] = "servicebus.windows.net:sastoken";
    request.ApplicationProperties["name"] = Fx.Format("amqp://{0}/{1}", sbNamespace, entity);
    cbsSender.Send(request);

    // receive hello response
    var response = cbsReceiver.Receive();
    if (response == null || response.Properties == null || response.ApplicationProperties == null)
    {
        result = false;
    }
    else
    {
        int statusCode = (int)response.ApplicationProperties["status-code"];
        if (statusCode != (int)HttpStatusCode.Accepted && statusCode != (int)HttpStatusCode.OK)
        {
            result = false;
        }
    }

    // hello sender/receiver may be kept open for refreshing tokens
    cbsSender.Close();
    cbsReceiver.Close();
    session.Close();

    return result;
}
```

Hello `PutCbsToken()` méthode reçoit hello *connexion* (instance de la classe connexion AMQP tel que fourni par hello [bibliothèque AMQP .NET Lite](https://github.com/Azure/amqpnetlite)) qui représente le service de toohello de connexion TCP hello et hello *sasToken* paramètre toosend de jeton SAS hello. 

> [!NOTE]
> Il est important que la connexion de hello est créée avec **le mécanisme d’authentification SASL définie tooEXTERNAL** (et pas hello brut par défaut avec le nom d’utilisateur et mot de passe utilisé lorsque vous n’avez pas besoin d’un jeton SAS toosend hello).
> 
> 

Ensuite, le serveur de publication hello crée deux liens AMQP pour envoyer un jeton SAS hello et la réception de réponse de hello (résultats de validation du jeton hello) à partir du service de hello.

message de type Hello AMQP contient un ensemble de propriétés et plus d’informations qu’un message simple. un jeton SAS Hello est corps hello de message de type hello (à l’aide de son constructeur). Hello **« ReplyTo »** propriété a la valeur nom du nœud toohello pour la réception du résultat de la validation hello sur lien du récepteur hello (vous pouvez modifier son nom si vous voulez, et elle est créée dynamiquement par le service de hello). trois propriétés d’application/custom Hello sont utilisées par hello service tooindicate quel type d’opération, il a tooexecute. Comme décrit par hello spécification préliminaire CBS, ils doivent être hello **nom de l’opération** (« put-jeton »), hello **type de jeton** (dans ce cas, un « servicebus.windows.net:sastoken ») et hello **» nom » de l’audience de hello** jeton de hello toowhich s’applique (entité toute entière de hello).

Après l’envoi d’un jeton SAS hello sur le lien de l’expéditeur hello, serveur de publication hello doit lire réponse hello sur lien du récepteur hello. réponse de Hello est un simple message AMQP avec une propriété d’application nommé **« code d’état »** qui peut contenir hello même valeurs sous la forme d’un code d’état HTTP.

## <a name="rights-required-for-service-bus-operations"></a>Droits requis pour les opérations Service Bus

Hello tableau suivant montre les droits d’accès hello requis pour effectuer diverses opérations sur les ressources Service Bus.

| Opération | Revendication obligatoire | Étendue de la revendication |
| --- | --- | --- |
| **Espace de noms** | | |
| Configure une règle d’autorisation dans un espace de noms |gérer |N’importe quelle adresse d’espace de noms |
| **Registre de service** | | |
| Énumération des stratégies privées |gérer |N’importe quelle adresse d’espace de noms |
| Commencer à écouter sur un espace de noms |Écouter |N’importe quelle adresse d’espace de noms |
| Écouteur de tooa de messages d’envoi à un espace de noms |Envoyer |N’importe quelle adresse d’espace de noms |
| **File d'attente** | | |
| Création d’une file d’attente |gérer |N’importe quelle adresse d’espace de noms |
| Suppression d'une file d'attente |gérer |N’importe quelle adresse de file d’attente valide |
| Énumérer les files d’attente |gérer |/$Resources/Queues |
| Obtenir la description de file d’attente hello |Gérer |N’importe quelle adresse de file d’attente valide |
| Configure une règle d’autorisation pour une file d’attente |gérer |N’importe quelle adresse de file d’attente valide |
| Envoyer en file d’attente toohello |Envoyer |N’importe quelle adresse de file d’attente valide |
| Réception des messages d'une file d'attente |Écouter |N’importe quelle adresse de file d’attente valide |
| Abandonner ou terminer les messages après avoir reçu le message de type hello en mode de verrou de lecture |Écouter |N’importe quelle adresse de file d’attente valide |
| Différer un message pour une récupération ultérieure |Écouter |N’importe quelle adresse de file d’attente valide |
| Mettre un message au rebut |Écouter |N’importe quelle adresse de file d’attente valide |
| Obtenir l’état hello associé à une session de file d’attente de messages |Écouter |N’importe quelle adresse de file d’attente valide |
| Définir l’état hello associé à une session de file d’attente de messages |Écouter |N’importe quelle adresse de file d’attente valide |
| **Rubrique** | | |
| Création d'une rubrique |gérer |N’importe quelle adresse d’espace de noms |
| Supprimer une rubrique |gérer |N’importe quelle adresse de rubrique valide |
| Énumérer les rubriques |gérer |/$Resources/Topics |
| Obtenir la description de la rubrique hello |Gérer |N’importe quelle adresse de rubrique valide |
| Configure une règle d’autorisation pour une rubrique |gérer |N’importe quelle adresse de rubrique valide |
| Envoyer toohello rubrique |Envoyer |N’importe quelle adresse de rubrique valide |
| **Abonnement** | | |
| Création d'un abonnement |gérer |N’importe quelle adresse d’espace de noms |
| Supprimer l’abonnement |gérer |../myTopic/Subscriptions/mySubscription |
| Énumérer les abonnements |gérer |../myTopic/Subscriptions |
| Obtenir la description de l’abonnement |Gérer |../myTopic/Subscriptions/mySubscription |
| Abandonner ou terminer les messages après avoir reçu le message de type hello en mode de verrou de lecture |Écouter |../myTopic/Subscriptions/mySubscription |
| Différer un message pour une récupération ultérieure |Écouter |../myTopic/Subscriptions/mySubscription |
| Mettre un message au rebut |Écouter |../myTopic/Subscriptions/mySubscription |
| Obtenir l’état hello associé à une session de rubrique |Écouter |../myTopic/Subscriptions/mySubscription |
| Définir l’état hello associé à une session de rubrique |Écouter |../myTopic/Subscriptions/mySubscription |
| **Règles** | | |
| Créer une règle |gérer |../myTopic/Subscriptions/mySubscription |
| Supprimer une règle |gérer |../myTopic/Subscriptions/mySubscription |
| Énumérer des règles |Gérer ou écouter |.. /myTopic/Subscriptions/mySubscription/Rules 

## <a name="next-steps"></a>Étapes suivantes

toolearn en savoir plus sur le Bus des services de messagerie, consultez hello rubriques suivantes.

* [Concepts de base de Service Bus](service-bus-fundamentals-hybrid-solutions.md)
* [Files d’attente, rubriques et abonnements Service Bus](service-bus-queues-topics-subscriptions.md)
* [Comment les files d’attente de toouse Service Bus](service-bus-dotnet-get-started-with-queues.md)
* [Comment toouse Service Bus rubriques et abonnements](service-bus-dotnet-how-to-use-topics-subscriptions.md)

[Azure portal]: https://portal.azure.com