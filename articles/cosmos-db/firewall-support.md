---
title: "contrôle d’accès prise en charge de pare-feu de base de données Cosmos aaaAzure & IP | Documents Microsoft"
description: "Découvrez comment toouse stratégies de contrôle d’accès IP pour le pare-feu prennent en charge sur les comptes de base de données de base de données Azure Cosmos."
keywords: "contrôle d’accès IP, prise en charge du pare-feu"
services: cosmos-db
author: shahankur11
manager: jhubbard
editor: 
tags: azure-resource-manager
documentationcenter: 
ms.assetid: c1b9ede0-ed93-411a-ac9a-62c113a8e887
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: ankshah
ms.openlocfilehash: b5cdbdb28e9d7ee0fd0ea54aad277167b699929f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-firewall-support"></a>Prise en charge du pare-feu Azure Cosmos DB
toosecure les données stockées dans un compte de base de données de base de données Azure Cosmos, Azure Cosmos DB a fourni le prise en charge pour une clé secrète en fonction [modèle d’autorisation](https://msdn.microsoft.com/library/azure/dn783368.aspx) qui utilise un code d’authentification forte message en fonction de hachage (HMAC). À présent, en outre toohello secret en fonction de modèle d’autorisation, base de données Azure Cosmos prend en charge basée sur des contrôles d’accès IP pour la prise en charge de pare-feu entrantes. Ce modèle est très similaire règles de pare-feu toohello d’un système de base de données traditionnelle et fournit un niveau supplémentaire de sécurité toohello compte de base de données de base de données Azure Cosmos. Avec ce modèle, vous pouvez désormais configurer une base de données Azure Cosmos de base de données compte toobe accessible uniquement à partir d’un jeu approuvé d’ordinateurs ou services de cloud computing. Accéder aux ressources de base de données Cosmos tooAzure à partir de ces jeux approuvées des ordinateurs et des services requièrent toujours hello appelant toopresent un jeton d’autorisation valide.

## <a name="ip-access-control-overview"></a>Vue d’ensemble du contrôle d’accès IP
Par défaut, un compte de base de données de base de données Azure Cosmos est accessible à partir de l’internet public tant que la demande de hello est accompagnée d’un jeton d’autorisation valide. contrôle d’accès stratégie tooconfigure IP, les utilisateur de hello doit fournir des ensemble hello d’adresses IP ou des plages d’adresses IP dans toobe de forme CIDR inclus en tant que hello autorisée de la liste des adresses IP de client pour un compte de base de données spécifique. Une fois cette configuration est appliquée, toutes les demandes provenant d’ordinateurs en dehors de cette liste autorisée seront bloqués par le serveur de hello.  connexion Hello flux de traitement d’hello contrôle d’accès basé sur IP est décrite dans hello suivant schéma.

![Diagramme illustrant le processus de connexion hello pour le contrôle d’accès basé sur IP](./media/firewall-support/firewall-support-flow.png)

## <a name="connections-from-cloud-services"></a>Connexions à partir de services cloud
Dans Azure, les services cloud sont une méthode très courante d’hébergement de la logique de service de couche intermédiaire à l’aide d’Azure Cosmos DB. tooan d’accès tooenable compte de base de données de base de données Azure Cosmos à partir d’un service cloud, hello adresse IP publique du service de cloud computing hello doit être ajouté toohello autorisée de la liste des adresses IP associées à votre compte de base de données de base de données Azure Cosmos par [configuration Hello de stratégie de contrôle d’accès IP](#configure-ip-policy).  Cela garantit que toutes les instances de rôle des services de cloud computing ont accès tooyour compte de base de données de base de données Azure Cosmos. Vous pouvez récupérer des adresses IP pour vos services cloud Bonjour portail Azure, comme indiqué dans hello suivant capture d’écran.

![Capture d’écran montrant l’adresse IP publique de hello pour un service cloud affichés dans hello portail Azure](./media/firewall-support/public-ip-addresses.png)

Lorsque vous faites évoluer votre service cloud en ajoutant une ou plusieurs instances de rôle supplémentaires, ces nouvelles instances auront automatiquement compte de base de données de base de données Azure Cosmos de toohello accès, car ils font partie de hello même service cloud.

## <a name="connections-from-virtual-machines"></a>Connexions à partir de machines virtuelles
[Machines virtuelles](https://azure.microsoft.com/services/virtual-machines/) ou [machines virtuelles identiques](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) peut également être utilisé toohost services de niveau intermédiaire à l’aide de la base de données Azure Cosmos.  tooconfigure hello Azure Cosmos DB de base de données compte tooallow l’accès à partir d’ordinateurs virtuels, les adresses IP publiques de machines virtuelles identiques et/ou de la machine virtuelle doit être configuré comme l’un des hello autorisée pour votre compte de base de données de base de données Azure Cosmos par des adresses IP [configuration de la stratégie de contrôle d’accès IP hello](#configure-ip-policy). Vous pouvez récupérer des adresses IP pour les ordinateurs virtuels dans hello portail Azure, comme indiqué dans hello suivant capture d’écran.

![Capture d’écran montrant une adresse IP publique pour un ordinateur virtuel affiché dans hello portail Azure](./media/firewall-support/public-ip-addresses-dns.png)

Lorsque vous ajoutez le groupe d’instances de machine virtuelle supplémentaire toohello, elles sont fournies automatiquement compte de base de données access tooyour base de données Azure Cosmos.

## <a name="connections-from-hello-internet"></a>Connexions à partir de hello internet
Lorsque vous avez accès à une base de données Azure Cosmos compte base de données à partir d’un ordinateur sur hello internet, hello adresse IP du client ou la plage d’adresses IP de l’ordinateur de hello doit être ajouté toohello liste d’adresses IP pour le compte de base de données de base de données Azure Cosmos de hello autorisée. 

## <a id="configure-ip-policy"></a>Configuration de la stratégie de contrôle d’accès IP hello
stratégie de contrôle d’accès Hello IP peut être définie dans hello portail Azure, ou par programmation via [CLI d’Azure](cli-samples.md), [Azure Powershell](powershell-samples.md), ou hello [API REST](/rest/api/documentdb/) en mettant à jour hello `ipRangeFilter` propriété. Les plages/adresses IP doivent être séparées par des virgules et ne doivent pas contenir d’espaces. Exemple : « 13.91.6.132,13.91.6.1/24 ». Lors de la mise à jour de votre compte de base de données à utiliser ces méthodes, être toopopulate que tous les tooprevent de propriétés hello la réinitialisation des paramètres de toodefault.

> [!NOTE]
> En activant une stratégie de contrôle d’accès IP pour votre compte de base de données de base de données Azure Cosmos, tous les accès tooyour compte de base de données de base de données Azure Cosmos à partir d’ordinateurs à l’extérieur de hello configuré autorisé la liste des plages d’adresses IP sont bloqués. En vertu de ce modèle, navigation opération hello de plan des données à partir du portail de hello sera également l’intégrité de hello tooensure bloqués de contrôle d’accès.

développement de toosimplify, hello portail Azure permet d’identifier et ajouter IP hello de votre toohello d’ordinateur client autorisée de la liste, afin que les applications qui s’exécutent de votre ordinateur peuvent accéder à hello compte de base de données Azure Cosmos. Notez que hello client ici l’adresse IP est détecté comme indiqué par le portail de hello. Il peut être adresse IP du client hello de votre ordinateur, mais elle peut également être hello adresseIP de votre passerelle de réseau. N’oubliez pas de tooremove avant le cours tooproduction.

stratégie de contrôle d’accès tooset hello IP Bonjour portail Azure, accédez Panneau de compte de base de données Azure Cosmos toohello, cliquez sur **pare-feu** dans le menu de navigation hello, puis cliquez sur **ON** 

![Capture d’écran montrant comment tooopen hello panneau pare-feu Bonjour portail Azure](./media/firewall-support/azure-portal-firewall.png)

Dans le volet de nouveau hello, spécifiez si hello portail Azure peut accéder au compte de hello, ajoutez d’autres adresses et plages si nécessaire, puis cliquez sur **enregistrer**.  

> [!NOTE]
> Lorsque vous activez une stratégie de contrôle d’accès IP, vous devez adresse IP de hello tooadd pourquoi l’accès toomaintain portail Azure. les adresses IP portails Hello sont :
> |Région|Adresse IP|
> |------|----------|
> |Toutes les régions, à l’exception de celles spécifiées ci-dessous| 104.42.195.92|
> |Allemagne|51.4.229.218|
> |Chine|139.217.8.252|
> |Gouvernement des États-Unis – Arizona|52.244.48.71|
>

![Capture d’écran montrant la façon dont les paramètres de pare-feu tooconfigure Bonjour portail Azure](./media/firewall-support/azure-portal-firewall-configure.png)

## <a name="troubleshooting-hello-ip-access-control-policy"></a>Résolution des problèmes de stratégie de contrôle d’accès hello IP
### <a name="portal-operations"></a>Opérations du portail
En activant une stratégie de contrôle d’accès IP pour votre compte de base de données de base de données Azure Cosmos, tous les accès tooyour compte de base de données de base de données Azure Cosmos à partir d’ordinateurs à l’extérieur de hello configuré autorisé la liste des plages d’adresses IP sont bloqués. Par conséquent, si vous souhaitez que les opérations de plan de données du portail tooenable à la navigation sur les collections et les documents de la requête, vous devez tooexplicitly autoriser l’accès de portail Azure à l’aide de hello **pare-feu** panneau dans le portail de hello. 

![Capture d’écran montrant comment tooenable accès toohello portail Azure](./media/firewall-support/azure-portal-access-firewall.png)

### <a name="sdk--rest-api"></a>Kit de développement logiciel (SDK) et API REST
Pour des raisons de sécurité, l’accès via le Kit de développement logiciel ou de l’API REST à partir d’ordinateurs pas sur la liste autorisée de hello renverra une réponse de 404 introuvable générique avec des détails supplémentaires. Vérifiez que hello IP autorisée liste configuré pour votre base de données Azure Cosmos de base de données compte tooensure hello stratégie correcte est appliquée tooyour compte de base de données de base de données Azure Cosmos.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur les conseils sur les performances relatives au réseau, consultez [Conseils relatifs aux performances](performance-tips.md).

