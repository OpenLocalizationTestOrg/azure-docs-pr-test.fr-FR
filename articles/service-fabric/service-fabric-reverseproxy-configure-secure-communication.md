---
title: "aaaAzure Service Fabric inverser une communication sécurisée proxy | Documents Microsoft"
description: "Configurer la communication de bout en bout sécurisée de proxy inverse tooenable."
services: service-fabric
documentationcenter: .net
author: kavyako
manager: vipulm
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/10/2017
ms.author: kavyako
ms.openlocfilehash: e1248dffe2c324373ad0d09d3f5f094db74480d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-secure-service-with-hello-reverse-proxy"></a>Connecter le service sécurisé tooa avec le proxy inverse hello

Cet article explique comment tooestablish sécuriser la connexion entre le proxy inverse de hello et services, permettant ainsi d’activer un canal sécurisé tooend de fin.

Connecter les services toosecure est pris en charge uniquement lorsque le proxy inverse est toolisten configuré sur le protocole HTTPS. Le reste du document de hello suppose que Hello cas.
Consultez trop[proxy dans Azure Service Fabric inverse](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) proxy inverse de tooconfigure hello dans Service Fabric.

## <a name="secure-connection-establishment-between-hello-reverse-proxy-and-services"></a>Établissement d’une connexion sécurisée entre le proxy inverse hello et des services 

### <a name="reverse-proxy-authenticating-tooservices"></a>Inverser le proxy de l’authentification tooservices :
Hello proxy inverse s’identifie en tooservices à l’aide de son certificat spécifié avec ***reverseProxyCertificate*** propriété Bonjour **Cluster** [section de ressources de type](../azure-resource-manager/resource-group-authoring-templates.md). Les services peuvent implémenter des certificats d’hello hello logique tooverify présenté par le proxy inverse de hello. services de Hello peuvent spécifier les détails du certificat client hello accepté en tant que paramètres de configuration dans le package de configuration hello. Cela peut être lu lors de l’exécution et utilisé toovalidate hello certificat est présenté par un proxy inverse de hello. Consultez trop[gérer les paramètres de l’application](service-fabric-manage-multiple-environment-app-configuration.md) paramètres de configuration tooadd hello. 

### <a name="reverse-proxy-verifying-hello-services-identity-via-hello-certificate-presented-by-hello-service"></a>Inverser la vérification de l’identité du service hello via certificat hello présenté par hello service de proxy :
validation du certificat de serveur tooperform de certificats hello présenté par les services de hello, proxy inverse prend en charge une des options suivantes de hello : None, ServiceCommonNameAndIssuer et ServiceCertificateThumbprints.
tooselect un de ces trois options, spécifiez hello **ApplicationCertificateValidationPolicy** dans la section de paramètres de hello d’élément passerelle/Http sous [fabricSettings](service-fabric-cluster-fabric-settings.md).

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "None"
              }
            ]
          }
        ],
        ...
}
```

Pour plus d’informations sur la configuration supplémentaire pour chacune de ces options, voir toohello la prochaine section.

### <a name="service-certificate-validation-options"></a>Options de validation du certificat de service 

- **Aucun**: proxy inverse ignore la vérification du certificat de service proxy hello et établit une connexion sécurisée hello. Il s’agit par défaut hello.
Spécifiez hello **ApplicationCertificateValidationPolicy** avec la valeur **aucun** dans la section des paramètres d’élément de la passerelle/Http hello.

- **ServiceCommonNameAndIssuer**: proxy inverse vérifie le certificat de hello présenté par le service hello basé sur le nom commun du certificat et l’empreinte numérique de l’émetteur immédiate : spécifiez hello **ApplicationCertificateValidationPolicy**  avec la valeur **ServiceCommonNameAndIssuer** dans la section des paramètres d’élément de la passerelle/Http hello.

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "ServiceCommonNameAndIssuer"
              }
            ]
          }
        ],
        ...
}
```

la liste hello toospecify de nom commun de service et les empreintes numériques de l’émetteur, ajoutez un **passerelle/Http/ServiceCommonNameAndIssuer** élément sous fabricSettings, comme indiqué ci-dessous. Plusieurs paires d’empreinte numérique de l’émetteur et de nom commun du certificat peuvent être ajoutés dans l’élément de tableau de paramètres hello. 

Si proxy inverse du point de terminaison hello se connecte toopresents un certificat qui est commun empreinte numérique du nom et de l’émetteur correspond à une des valeurs hello spécifiés ici, le canal SSL est établi. Sur les détails du certificat échec toomatch hello, proxy inverse échoue demande du client hello avec un code d’état 502 (passerelle incorrecte). ligne d’état HTTP de Hello contient également une expression de hello « Certificat SSL non valide ». 

```json
{
"fabricSettings": [
          ...
          {
             "name": "ApplicationGateway/Http/ServiceCommonNameAndIssuer",
            "parameters": [
              {
                "name": "WinFabric-Test-Certificate-CN1",
                "value": "b3 44 9b 01 8d 0f 68 39 a2 c5 d6 2b 5b 6c 6a c8 22 b4 22 11"
              },
              {
                "name": "WinFabric-Test-Certificate-CN2",
                "value": "b3 44 9b 01 8d 0f 68 39 a2 c5 d6 2b 5b 6c 6a c8 22 11 33 44"
              }
            ]
          }
        ],
        ...
}
```


- **ServiceCertificateThumbprints**: proxy inverse vérifiera le certificat de service proxy hello en fonction de son empreinte. Vous pouvez choisir toogo cet itinéraire lorsque les services de hello sont configurés avec des certificats auto-signés : spécifiez hello **ApplicationCertificateValidationPolicy** avec la valeur **ServiceCertificateThumbprints**dans la section des paramètres d’élément de la passerelle/Http hello.

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "ServiceCertificateThumbprints"
              }
            ]
          }
        ],
        ...
}
```

Spécifiez également les empreintes numériques de hello avec un **ServiceCertificateThumbprints** entrée sous la section Paramètres de l’élément de la passerelle/Http. Plusieurs empreintes numériques peuvent être spécifiés comme une liste séparée par des virgules dans le champ de valeur hello, comme indiqué ci-dessous :

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
                ...
              {
                "name": "ServiceCertificateThumbprints",
                "value": "78 12 20 5a 39 d2 23 76 da a0 37 f0 5a ed e3 60 1a 7e 64 bf,78 12 20 5a 39 d2 23 76 da a0 37 f0 5a ed e3 60 1a 7e 64 b9"
              }
            ]
          }
        ],
        ...
}
```

Si l’empreinte numérique hello hello du certificat de serveur est répertorié dans cette entrée de configuration, le proxy inverse réussit connexion SSL de hello. Sinon, elle met fin à la connexion de hello et échoue hello demande du client avec un 502 (passerelle incorrecte). ligne d’état HTTP de Hello contient également une expression de hello « Certificat SSL non valide ».

## <a name="endpoint-selection-logic-when-services-expose-secure-as-well-as-unsecured-endpoints"></a>Logique de sélection du point de terminaison quand les services exposent des points de terminaison sécurisés et non sécurisés
Service Fabric prend en charge la configuration de plusieurs points de terminaison pour un service. Voir [Spécifier des ressources dans un manifeste de service](service-fabric-service-manifest-resources.md).

Proxy inverse sélectionne l’une des hello points de terminaison tooforward hello demande selon hello **ListenerName** paramètre de requête. S’il n’est pas spécifié, choisir n’importe quel point de terminaison à partir de la liste de points de terminaison hello. Maintenant, il peut s’agir d’un point de terminaison HTTP ou HTTPS. Il peut y avoir des scénarios/exigences où vous souhaitez toooperate de proxy inverse hello en « seul mode sécurisé », c'est-à-dire Vous ne souhaitez pas hello proxy inverse sécurisé tooforward demandes toounsecured points de terminaison. Cela peut être obtenue en spécifiant hello **SecureOnlyMode** entrée de configuration avec la valeur **true** dans la section des paramètres d’élément de la passerelle/Http hello.   

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
                ...
              {
                "name": "SecureOnlyMode",
                "value": true
              }
            ]
          }
        ],
        ...
}
```

> 
> En **SecureOnlyMode**, si le client a spécifié un **ListenerName** correspondant tooan HTTP(unsecured) point de terminaison, le proxy inverse échoue demande hello avec un code d’état 404 (introuvable) de HTTP.

## <a name="setting-up-client-certificate-authentication-through-hello-reverse-proxy"></a>Configuration de l’authentification de certificat client via le proxy inverse hello
Terminaison SSL se produit au proxy inverse de hello et toutes les données de certificat de client hello est perdue. Pour hello services tooperform authentification par certificat client, définissez hello **ForwardClientCertificate** définition dans la section Paramètres de hello d’élément de la passerelle/Http.

1. Lorsque **ForwardClientCertificate** est défini trop**false**, inverser proxy ne nécessite pas de certificat de client hello pendant la négociation SSL avec le client de hello.
Il s’agit par défaut hello.

2. Lorsque **ForwardClientCertificate** est défini trop**true**, inverser les requêtes de proxy pour le certificat du client hello pendant la négociation SSL avec le client de hello.
Puis transmettra les client hello des données de certificat dans un en-tête HTTP personnalisé nommé **X-Client-certificat**. valeur d’en-tête Hello est la chaîne de format PEM hello codé en base64 du certificat du client hello. service de Hello peut réussir/échec demande hello avec le code d’état approprié après avoir inspecté les données de certificat hello.
Si le client de hello ne présente pas un certificat, proxy inverse transfère un en-tête vide et laissez les cas de hello hello service handle.

> Le proxy inverse est un simple redirecteur. Il n’exécute aucune validation de certificat du client hello.


## <a name="next-steps"></a>Étapes suivantes
* Consultez trop[configurer les services de proxy inverse tooconnect toosecure](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) exemples de modèle pour le Gestionnaire de ressources Azure tooconfigure un proxy inverse sécurisée avec les options de validation de certificat de service différent hello.
* Pour obtenir un exemple de communication HTTP entre services, consultez cet [exemple de projet sur GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).
* [Appels de procédure distante avec Reliable Services à distance](service-fabric-reliable-services-communication-remoting.md)
* [API Web qui utilise OWIN dans Reliable Services](service-fabric-reliable-services-communication-webapi.md)
* [Gérer les certificats de cluster](service-fabric-cluster-security-update-certs-azure.md)
