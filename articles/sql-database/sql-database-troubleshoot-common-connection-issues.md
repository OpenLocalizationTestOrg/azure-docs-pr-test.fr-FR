---
title: "tooAzure de problèmes de connexion courantes aaaTroubleshoot base de données SQL"
description: "Étapes tooidentify et résoudre les connexions erreurs courantes pour la base de données SQL Azure."
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: ac463d1c-aec8-443d-b66e-fa5eadcccfa8
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: eb5f2d7b123a76942c7e4a84a7f475344fbcb144
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-connection-issues-tooazure-sql-database"></a>Résoudre les problèmes de connexion tooAzure de la base de données SQL
En cas d’échec de la connexion de hello tooAzure base de données SQL, vous recevez [les messages d’erreur](sql-database-develop-error-messages.md). Cet article est une rubrique centralisée qui vous permet de résoudre les problèmes de connectivité des bases de données SQL Azure. Il introduit [hello des causes courantes](#cause) de problèmes de connexion, vous recommande de [un outil de dépannage](#try-the-troubleshooter-for-azure-sql-database-connectivity-issues) qui vous permet de problème de hello identité et fournit la résolution des problèmes étapes toosolve [ erreurs temporaires](#troubleshoot-transient-errors) et [erreurs persistants ou non temporaire](#troubleshoot-persistent-errors). 

Si vous rencontrez des problèmes de connexion de hello, essayez de hello résoudre les étapes décrites dans cet article.
[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="cause"></a>Cause :
Problèmes de connexion peuvent être dû à un des éléments suivants de hello :

* Échec tooapply meilleures pratiques et les règles de conception pendant le processus de conception d’application hello.  Consultez [vue d’ensemble du développement de base de données SQL](sql-database-develop-overview.md) tooget a démarré.
* Reconfiguration de la base de données SQL Azure
* Paramètres du pare-feu
* Expiration du délai de connexion
* Informations de connexion incorrectes
* Dépassement de la limite maximale sur certaines ressources de la base de données SQL Azure

En règle générale, tooAzure de problèmes de connexion de base de données SQL peut être classé comme suit :

* [Erreurs temporaires (de courte durée ou intermittentes)](#troubleshoot-transient-errors)
* [Erreurs persistantes ou non temporaires (erreurs qui se produisent régulièrement)](#troubleshoot-persistent-errors)

## <a name="try-hello-troubleshooter-for-azure-sql-database-connectivity-issues"></a>Essayez de résolution des problèmes hello pour les problèmes de connectivité de base de données SQL Azure
Si vous rencontrez une erreur de connexion spécifique, essayez [cet outil](https://support.microsoft.com/help/10085/troubleshooting-connectivity-issues-with-microsoft-azure-sql-database), qui vous aidera à identifier et à résoudre rapidement votre problème.

## <a name="troubleshoot-transient-errors"></a>Résoudre les erreurs temporaires

Lorsqu’une application connecte à base de données SQL Azure tooan, vous recevez hello message d’erreur suivant :

```
Error code 40613: "Database <x> on server <y> is not currently available. Please retry hello connection later. If hello problem persists, contact customer support, and provide them hello session tracing ID of <z>"
```

> [!NOTE]
> Ce message d’erreur est généralement temporaire (de courte durée).
> 
> 

Cette erreur se produit lorsque hello est en cours d’une base de données Azure déplacé (ou reconfiguré) et votre application perd sa base de données SQL de connexion toohello. Les événements de reconfiguration de la base de données SQL sont liés à un événement planifié (par exemple, une mise à niveau logicielle) ou à un événement non planifié (par exemple, un arrêt de processus ou un équilibrage de charge). La plupart des événements de reconfiguration sont généralement de courte durée et se terminent en l’espace de 60 secondes maximum. Toutefois, ces événements peuvent s’occasionnellement toofinish plus de temps, telles que lorsqu’une transaction de grande taille entraîne une récupération à long terme.

### <a name="steps-tooresolve-transient-connectivity-issues"></a>Problèmes de connectivité temporaire tooresolve étapes

1. Vérifiez hello [tableau de bord de Service Microsoft Azure](https://azure.microsoft.com/status) pour toutes les interruptions connues qui s’est produite pendant le temps de hello pendant le hello les erreurs sont signalées par l’application hello.
2. Applications qui se connectent tooa le service cloud, telles que la base de données SQL Azure doit attendre les événements de reconfiguration périodiques et implémenter recommencez logique toohandle ces erreurs au lieu des surfaces d’en tant qu’application erreurs toousers. Hello de révision [erreurs temporaires](sql-database-connectivity-issues.md) hello section meilleures pratiques et concevoir des instructions à [vue d’ensemble du développement de base de données SQL](sql-database-develop-overview.md) pour plus d’informations générales des stratégies de nouvelle tentative. Passez ensuite en revue les exemples de code dans l’article [Bibliothèques de connexions pour SQL Database et SQL Server](sql-database-libraries.md) pour obtenir des informations spécifiques.
3. Une base de données approche de ses limites de ressources, il peut sembler toobe un problème de connectivité temporaire. Consultez la page [Résolution des problèmes de performances](sql-database-troubleshoot-performance.md).
4. Si des problèmes de connectivité se poursuivre, ou si hello durée pour laquelle votre application rencontre des erreurs de hello dépasse 60 secondes ou si vous voyez plusieurs occurrences de l’erreur de hello dans un jour donné, une demande de support Azure de fichiers en sélectionnant **obtenir prend en charge les** sur hello [prise en charge Azure](https://azure.microsoft.com/support/options) site.

## <a name="troubleshoot-persistent-errors"></a>Résoudre les erreurs persistantes
En cas d’application hello persistante tooconnect tooAzure base de données SQL, il indique généralement un problème avec l’un des éléments suivants de hello :

* Configuration du pare-feu. pare-feu de base de données ou côté client de SQL Azure Hello bloque les connexions tooAzure base de données SQL.
* Réseau de reconfiguration côté client de hello : par exemple, une nouvelle adresse IP ou un serveur proxy.
* Erreur de l’utilisateur : par exemple, saisi correctement les paramètres de connexion, telles que le nom de serveur hello dans la chaîne de connexion hello.

### <a name="steps-tooresolve-persistent-connectivity-issues"></a>Problèmes de connectivité persistant tooresolve étapes
1. Configurer [des règles de pare-feu](sql-database-configure-firewall-settings.md) tooallow adresse IP client en hello. Pour des raisons de tests temporaires, définir une règle de pare-feu à l’aide de 0.0.0.0 comme hello plage d’adresses IP de début et à l’aide de 255.255.255.255 comme hello fin de la plage d’adresses IP. Adresses IP tooall hello s’ouvre. Si elle résout votre problème de connectivité, supprimez cette règle et créez une règle de pare-feu pour une adresse ou une plage d’adresses IP correctement bornée. 
2. Sur tous les pare-feu entre le client de hello et hello Internet, assurez-vous que le port 1433 est ouvert pour les connexions sortantes. Révision [configurer le pare-feu Windows de hello tooAllow accès à SQL Server](https://msdn.microsoft.com/library/cc646023.aspx) et [hybride identité requis Ports et protocoles](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-ports) des pointeurs supplémentaires liés tooadditional ports que vous avez besoin de tooopen pour Authentification Azure Active Directory.
3. Vérifiez votre chaîne de connexion et d’autres paramètres de connexion. Consultez hello section de chaîne de connexion dans hello [rubrique des problèmes de connectivité](sql-database-connectivity-issues.md#connections-to-azure-sql-database).
4. Vérifiez l’intégrité du service dans le tableau de bord hello. Si vous pensez qu’une panne régionale, consultez [récupérer à partir d’une panne](sql-database-disaster-recovery.md) pour une nouvelle région étapes toorecover tooa.

## <a name="next-steps"></a>Étapes suivantes
* [Résoudre les problèmes de performances des bases de données SQL Azure](sql-database-troubleshoot-performance.md)
* [Documentation de hello Search sur Microsoft Azure](http://azure.microsoft.com/search/documentation/)
* [Hello d’affichage des dernières mises à jour de service de base de données SQL Azure toohello](http://azure.microsoft.com/updates/?service=sql-database)

## <a name="additional-resources"></a>Ressources supplémentaires
* [Vue d’ensemble du développement de base de données SQL](sql-database-develop-overview.md)
* [Aide générale sur le traitement des erreurs temporaires](../best-practices-retry-general.md)
* [Bibliothèques de connexions pour SQL Database et SQL Server](sql-database-libraries.md)

