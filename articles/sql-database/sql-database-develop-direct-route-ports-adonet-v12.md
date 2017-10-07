---
title: "aaaPorts au-delà de 1433 pour la base de données SQL | Documents Microsoft"
description: "Parfois, les connexions client à partir d’ADO.NET tooAzure base de données SQL ignorer hello proxy et interagissent directement avec la base de données hello. Les ports autres que le port 1433 deviennent importants."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.assetid: 3f17106a-92fd-4aa4-b6a9-1daa29421f64
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: sstein
ms.openlocfilehash: a35ff2d827ae3fa29b3ea855dbb7ed78583c82eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="ports-beyond-1433-for-adonet-45"></a>Ports au-delà de 1433 pour ADO.NET 4.5
Cette rubrique décrit le comportement de connexion de base de données SQL Azure hello pour les clients qui utilisent ADO.NET 4.5 ou version ultérieure. 

> [!IMPORTANT]
> Pour plus d’informations sur l’architecture de connectivité, consultez [Azure SQL Database connectivity architecture](sql-database-connectivity-architecture.md) (Architecture de connectivité d’Azure SQL Database).
>

## <a name="outside-vs-inside"></a>À l’extérieur et à l’intérieur
Pour les connexions tooAzure base de données SQL, nous devons tout d’abord demander si votre programme client s’exécute *en dehors de* ou *à l’intérieur de* limite de cloud computing Azure hello. les sous-sections Hello présentent deux scénarios courants.

#### <a name="outside-client-runs-on-your-desktop-computer"></a>*À l’extérieur :* le client s’exécute sur votre ordinateur de bureau
Le port 1433 est hello seul le port qui doit être ouvert sur votre ordinateur de bureau qui héberge votre application cliente de base de données SQL.

#### <a name="inside-client-runs-on-azure"></a>*À l’intérieur :* le client s’exécute sur Azure
Lorsque votre client s’exécute à l’intérieur des limites de cloud computing Azure hello, il utilise ce que nous pouvons appeler un *itinéraire direct* toointeract avec le serveur de base de données SQL hello. Une fois une connexion est établie, d’autres interactions entre le client de hello et la base de données n’impliquent aucun proxy de l’intergiciel (middleware).

séquence de Hello est comme suit :

1. ADO.NET 4.5 (ou version ultérieure) initie une interaction brève avec hello cloud Azure et reçoit un numéro de port identifié de manière dynamique.
   
   * numéro de port Hello identifié de manière dynamique est hello de 11000-11999 ou 14000-14999.
2. ADO.NET se connecte ensuite serveur de base de données SQL toohello directement avec aucun intergiciel (middleware) entre les deux.
3. Les requêtes sont envoyées directement toohello de base de données, et les résultats sont retournés directement toohello client.

Vérifiez que ce port hello plages de 11000-11999 et 14000-14999 sur votre ordinateur client Azure restent disponibles pour les interactions du client ADO.NET 4.5 avec la base de données SQL.

* En particulier, les ports dans la plage de hello doivent être de n’importe quel autre bloqueur sortant.
* Sur votre machine virtuelle Azure, hello **pare-feu Windows avec fonctions avancées de sécurité** contrôles hello des paramètres de port.
  
  * Vous pouvez utiliser hello [interface utilisateur du pare-feu](http://msdn.microsoft.com/library/cc646023.aspx) tooadd une règle pour lesquels vous spécifiez hello **TCP** telles que le protocole ainsi que d’une plage de ports avec la syntaxe hello **11000-11999**.

## <a name="version-clarifications"></a>Précisions concernant les versions
Cette section clarifie les monikers hello qui font référence à des versions tooproduct. Elle répertorie également certaines paires de versions entre les produits.

#### <a name="adonet"></a>ADO.NET
* ADO.NET 4.0 prend en charge le protocole de hello TDS 7.3, mais pas 7.4.
* ADO.NET 4.5 et versions ultérieures prend en charge le protocole de hello TDS 7.4.

## <a name="related-links"></a>Liens connexes
* ADO.NET 4.6 a été publié le 20 juillet 2015. Annonce de blog à partir de l’équipe de .NET hello est disponible [ici](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).
* ADO.NET 4.5 a été publié le 15 août 2012. Annonce de blog à partir de l’équipe de .NET hello est disponible [ici](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).
  
  * Un billet de blog sur ADO.NET 4.5.1 est disponible [ici](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).
* [Liste des versions du protocole TDS](http://www.freetds.org/userguide/tdshistory.htm)
* [Vue d’ensemble du développement de base de données SQL](sql-database-develop-overview.md)
* [Pare-feu Azure SQL Database](sql-database-firewall-configure.md)
* [Configuration des paramètres du pare-feu sur une base de données SQL](sql-database-configure-firewall-settings.md)

