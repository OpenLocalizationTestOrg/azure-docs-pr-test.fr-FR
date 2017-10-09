---
title: aaaSQL Azure avec Azure RemoteApp | Documents Microsoft
description: "Découvrez comment toouse SQL Azure avec Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
editor: 
ms.assetid: 35f81d75-bfd7-4980-807e-00339f2cb2a4
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: fec4cb1f1ab3cde03b6ff613650e01bae3552824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-azure-with-azure-remoteapp"></a>SQL Azure avec Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Souvent lorsque les clients choisissent toohost leurs applications Windows dans le cloud hello avec Azure RemoteApp ils veulent également toomigrate leurs données tels que les serveurs SQL en hello cloud pour un déploiement de cloud entière. Cela permet à la solution hébergée en totalité sur le cloud d’être accessible à tout moment par le biais de n’importe quel appareil, n’importe où à l’aide d’Azure RemoteApp. Ci-dessous sont des liens et des références, ainsi que des conseils toohelp vous avec ce processus.  

## <a name="migrate-your-sql-data"></a>Migrer vos données SQL
Démarrer avec [un tooAzure de base de données SQL Server de la base de données SQL de la migration](../sql-database/sql-database-cloud-migrate.md). 

## <a name="configure-azure-remoteapp"></a>Configuration d’Azure RemoteApp
Hébergez votre application Windows dans Azure RemoteApp. Vous trouverez ci-dessous une procédure étape par étape de très haut niveau :

1. Créer hello [Azure RemoteApp modèle VM](remoteapp-imageoptions.md). 
2. Installez application hello requis sur hello machine virtuelle.
3. Configurer l’application hello afin qu’il connecte toohello base de données SQL et vérifiez qu’elle fonctionne.
4. Sysprep et arrêtez hello machine virtuelle. Enregistrez cet élément sous forme d’image pour l’utiliser avec Azure. **Remarque :** vous devez tooensure qu’application hello est tooretain en mesure d’informations de connectivité hello DB via le processus de sysprep hello. Si application hello est tooretain ne peut pas les informations de connexion hello DB, vous pourriez fournisseur hello tooengage hello application toocheck comment nous pouvons spécifier la chaîne de connexion hello.
5. Importer l’image personnalisée de hello dans votre bibliothèque Azure RemoteApp en sélectionnant hello bon emplacement géographique que votre déploiement SQL Azure se trouve. 
6. Déployer une collection RemoteApp Bonjour même datacenter en tant que votre déploiement SQL Azure à l’aide de hello au-dessus de modèle et publier l’application hello. Déploiement d’Azure RemoteApp Bonjour même centre de données que votre déploiement SQL Azure permet de garantir des vitesses de connexion plus rapide hello et réduire la latence. 

## <a name="app-and-sql-configuration-considerations"></a>Considérations relatives à la configuration d’application et de SQL :
Il existe quelques points tooconsider lors de l’utilisation de SQL Azure avec RemoteApp :

En savoir plus [comment tooconfigure SQL Azure de base de données pare-feu](../sql-database/sql-database-firewall-configure.md). Un extrait des États de l’article hello, » au départ, tous les accès tooyour base de données SQL Azure serveur est bloqué par le pare-feu hello. Dans toobegin de commande à l’aide de votre serveur de base de données SQL Azure, vous devez aller toohello portail classique et spécifier une ou plusieurs règles de pare-feu de niveau serveur qui permettent l’accès tooyour base de données SQL Azure. Utilisez toospecify de règles de pare-feu hello quelle adresse IP comprise entre hello Internet sont autorisées, ou non des applications Azure peuvent essayer de serveur de base de données SQL Azure tooconnect tooyour. »

Également, lorsqu’un ordinateur tente de serveur de base de données tooconnect tooyour de hello Internet, pare-feu de hello vérifie si hello adresse IP de demande hello par rapport à l’ensemble complet de hello au niveau du serveur d’origine (si nécessaire) et les règles de pare-feu de niveau de base de données. « Si l’adresse IP de hello de demande de hello est dans une des plages de hello spécifiées dans les règles de pare-feu de niveau serveur hello, hello est accordé connexion serveur de base de données SQL Azure tooyour. » Par conséquent, nous pouvons utiliser des plages d’adresses IP, et pas uniquement des adresses IP source individuelles.

Suivez les instructions étape par étape de hello dans [Comment : configurer les paramètres de pare-feu sur la base de données SQL à l’aide de hello Azure Portal](../sql-database/sql-database-configure-firewall-settings.md) plage d’adresses IP toospecify hello. Lorsque vous configurez des règles de pare-feu SQL hello, veuillez fournir hello plage d’IP hello sous-réseau qui est spécifié pour hello collection Azure RemoteApp. Cela doit autoriser les serveurs de ARA hello tooconnect toohello base de données SQL même si elles seront-affectés de manière dynamique des adresses IP.

## <a name="troubleshooting"></a>Résolution des problèmes
Si vous rencontrez de hello d’à l’aide d’une application cliente hébergée dans Azure RemoteApp qui se connecte tooa SQL de base de données où hébergé sur Azure ou localement est lente il peut y avoir plusieurs raisons pour lesquelles.  

* Latence du réseau à partir de votre tooAzure de périphérique est élevée. Déplacer toohello mieux et connexion plus rapide que vous pouvez pour de meilleures performances. Utilisez [azurespeed.com](http://azurespeed.com/) comme un tootest outil général de votre appareils latence tooAzure Datacenter.  
* L’application cliente hébergée dans Azure RemoteApp est surchargée. En sélectionnant un autre plan de facturation, par exemple, la facturation Premium, vous pouvez améliorer les performances. Une autre astuce consiste aux ressources de hello toomonitor votre application consomme : pendant une session active, effectuer une séquence de touches ctrl-alt-fin qui exécutera hello SAS de l’écran, sélectionnez le Gestionnaire des tâches et observer l’utilisation des ressources pour votre application.
* SQL Server est surchargé ou n’est pas optimisé. Suivez les instructions SQL pour le dépannage. 

