---
title: "paramètres KVSActorStateProvider aaaChange microservices Azure | Documents Microsoft"
description: "Découvrez comment configurer les acteurs avec état Azure Service Fabric de type KVSActorStateProvider."
services: Service-Fabric
documentationcenter: .net
author: sumukhs
manager: timlt
editor: 
ms.assetid: dbed72f4-dda5-4287-bd56-da492710cd96
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: sumukhs
ms.openlocfilehash: e003512678556e68a8926b1b9c6c28d9ae3979d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-reliable-actors--kvsactorstateprovider"></a>Configuration de Reliable Actors - KVSActorStateProvider
Vous pouvez modifier la configuration par défaut de hello de KVSActorStateProvider en modifiant le fichier settings.xml hello qui est généré dans la racine du package Microsoft Visual Studio hello dans le dossier de configuration hello pour l’acteur spécifiés de hello.

Bonjour Azure Service Fabric runtime recherche des noms de section prédéfinie dans le fichier settings.xml de hello et consomme les valeurs de configuration hello lors de la création de hello sous-jacent des composants d’exécution.

> [!NOTE]
> Faire **pas** supprimer ou modifier les noms de section hello Hello suivant des configurations dans le fichier settings.xml hello généré Bonjour solution Visual Studio.
> 
> 

## <a name="replicator-security-configuration"></a>Configuration de la sécurité du réplicateur
Configurations de sécurité réplicateur sont un canal de communication utilisé toosecure hello est utilisé lors de la réplication. Cela signifie que les services ne peut pas voir l’autre trafic de réplication, garantissant que les données de salutation hautement disponible sont également sécurisées.
Par défaut, une section de configuration de sécurité vide empêche de sécuriser la réplication.

### <a name="section-name"></a>Nom de la section
&lt;ActorName&gt;ServiceReplicatorSecurityConfig

## <a name="replicator-configuration"></a>Configuration du réplicateur
Configurations de réplicateur configurer réplicateur hello qui est responsable de l’état de fournisseur d’état d’acteur hello hautement fiable.
configuration par défaut de Hello est générée par le modèle de Visual Studio hello et suffisante. Cette section décrit les configurations supplémentaires qui sont le réplicateur de hello tootune disponibles.

### <a name="section-name"></a>Nom de la section
&lt;ActorName&gt;ServiceReplicatorConfig

### <a name="configuration-names"></a>Noms des configurations
| Nom | Unité | Valeur par défaut | Remarques |
| --- | --- | --- | --- |
| BatchAcknowledgementInterval |Secondes |0.015 |Période de temps pour le réplicateur hello au temps d’attente secondaire hello après la réception d’une opération avant le renvoi d’un toohello d’accusé de réception principal. Toutes les autres toobe d’accusés de réception envoyé pour les opérations de traitement dans cet intervalle sont envoyés sous la forme d’une réponse. |
| ReplicatorEndpoint |N/A |Aucune valeur par défaut (paramètre obligatoire) |Adresse IP et port qui hello principal/secondaire réplicateur utilisera toocommunicate avec autres duplicateurs hello jeu de réplicas. Cela doit faire référence à un point de terminaison TCP ressource de manifeste de service hello. Consultez trop[les ressources de manifeste de Service](service-fabric-service-manifest-resources.md) tooread plus d’informations sur la définition des ressources d’un point de terminaison dans le manifeste de service hello. |
| RetryInterval |Secondes |5 |Période après les hello réplicateur nouveau transmet un message si elle ne reçoit pas d’accusé de réception pour une opération. |
| MaxReplicationMessageSize |Octets |50 Mo |Taille maximale des données de réplication pouvant être transmises dans un même message. |
| MaxPrimaryReplicationQueueSize |Nombre d'opérations |1 024 |Nombre maximal d’opérations dans la file d’attente principale de hello. Une opération est libérée après que Réplicateur principal de hello reçoit un accusé de réception auprès de tous les fabricants de hello secondaire. Cette valeur doit être supérieure à 64 et être une puissance de 2. |
| MaxSecondaryReplicationQueueSize |Nombre d'opérations |2 048 |Nombre maximal d’opérations dans la file d’attente secondaire de hello. Une opération est libérée une fois son état devenu hautement disponible grâce à la persistance. Cette valeur doit être supérieure à 64 et être une puissance de 2. |

## <a name="store-configuration"></a>Configuration du magasin
Magasin de configurations sont utilisées tooconfigure hello banque d’état hello toopersist utilisé qui est en cours de réplication.
configuration par défaut de Hello est générée par le modèle de Visual Studio hello et suffisante. Cette section décrit les configurations supplémentaires qui sont le magasin local de hello tootune disponibles.

### <a name="section-name"></a>Nom de la section
&lt;ActorName&gt;ServiceLocalStoreConfig

### <a name="configuration-names"></a>Noms des configurations
| Nom | Unité | Valeur par défaut | Remarques |
| --- | --- | --- | --- |
| MaxAsyncCommitDelayInMilliseconds |Millisecondes |200 |Définit un maximum de hello intervalle pour les validations du magasin local fiable de traitement par lot. |
| MaxVerPages |Nombre de pages |16 384 |nombre maximal de Hello de pages de version Bonjour local stocker la base de données. Il détermine le nombre maximal de hello de transactions en attente. |

## <a name="sample-configuration-file"></a>Exemple de fichier de configuration
```xml
<?xml version="1.0" encoding="utf-8"?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Section Name="MyActorServiceReplicatorConfig">
      <Parameter Name="ReplicatorEndpoint" Value="MyActorServiceReplicatorEndpoint" />
      <Parameter Name="BatchAcknowledgementInterval" Value="0.05"/>
   </Section>
   <Section Name="MyActorServiceLocalStoreConfig">
      <Parameter Name="MaxVerPages" Value="8192" />
   </Section>
   <Section Name="MyActorServiceReplicatorSecurityConfig">
      <Parameter Name="CredentialType" Value="X509" />
      <Parameter Name="FindType" Value="FindByThumbprint" />
      <Parameter Name="FindValue" Value="9d c9 06 b1 69 dc 4f af fd 16 97 ac 78 1e 80 67 90 74 9d 2f" />
      <Parameter Name="StoreLocation" Value="LocalMachine" />
      <Parameter Name="StoreName" Value="My" />
      <Parameter Name="ProtectionLevel" Value="EncryptAndSign" />
      <Parameter Name="AllowedCommonNames" Value="My-Test-SAN1-Alice,My-Test-SAN1-Bob" />
   </Section>
</Settings>
```
## <a name="remarks"></a>Remarques
paramètre de BatchAcknowledgementInterval Hello contrôle la latence de réplication. La valeur '0' entraîne hello latence minimale, au coût de hello de débit (comme les autres messages d’accusé de réception doivent être envoyées et traitées, contenant chacune des accusés de réception moins).
Hello plus grande valeur hello pour BatchAcknowledgementInterval, hello hello plu globale débit de la réplication, au coût de hello de latence d’opération plus élevée. Cela traduit directement toohello une latence de transaction est validée.

