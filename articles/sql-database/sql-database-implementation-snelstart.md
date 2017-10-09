---
title: "aaaAzure étude de cas de base de données Azure SQL - Snelstart | Documents Microsoft"
description: "Découvrez comment toorapidly de base de données SQL utilise SnelStart étendu ses services d’entreprise à un taux de 1 000 nouvelles Azure SQL bases de données par mois"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: fab506b2-439d-4f1a-bdc5-d1d25c80d267
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 69572393f41a9baf44f41b4f5f4ebbef347de851
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="with-azure-snelstart-has-rapidly-expanded-its-business-services-at-a-rate-of-1000-new-azure-sql-databases-per-month"></a>Avec Azure, SnelStart a rapidement développé ses services d’entreprise au rythme de 1 000 nouvelles bases de données Azure SQL Database par mois
![Logo SnelStart](./media/sql-database-implementation-snelstart/snelstartlogo.png)

SnelStart rend hello pays-bas populaires financières et entreprise-logiciel de gestion pour les petites et moyennes entreprises (SMB). Une équipe de 110 employés, dont 35 dans le service informatique, est au service de ses 55 000 clients. En déplaçant d’offre de software-as-a-service (SaaS) tooa de logiciels de bureau reposant sur Azure, SnelStart apportées hello plus de services intégrés, automatiser la gestion de l’environnement familier en c# et l’optimisation des performances et l’évolutivité par ni over - ou entreprises sous la mise en service à l’aide de pools élastiques. À l’aide de Azure fournit fluidité de hello SnelStart de déplacement de clients locaux et hello cloud.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-Case-Study-SnelStart/player]
> 
> 

## <a name="why-snelstart-extended-services-from-hello-desktop-toohello-cloud"></a>Pourquoi SnelStart étendus des services de cloud de bureau toohello hello
> « Travail avec Azure signifie que nous pouvons fournir des logiciels plus rapidement, rapidement réagissent toocustomer demandes et des solutions à l’échelle lorsque demandes augmentent. »
> 
> — Henry Been, architecte logiciel
> 
> 

SnelStart gère avec succès des activités logicielles depuis des années, selon un modèle de développement traditionnel : codage, empaquetage, livraison et ainsi de suite. Au fil du temps, hello rythme de modification ont augmenté plus rapidement et plus rapide. Réglementations fréquemment modifiés, et les clients nécessaire plus facile façons tooprocess financiers et collaborent avec leurs comptables et le gouvernement tookeep des ces modifications.

« Expédition logiciel toocustomers était coûteux et limitation, » selon tooHenry été, architecte de logiciels. Les coûts de production, d’empaquetage et de livraison limitaient la fréquence à laquelle nous pouvions sortir des logiciels. Nous avons dû toopackage les mises à jour des expéditions périodiques, mais qui rend difficile toomeet nos clients la modification de vos besoins. Nous avons jamais être assurés que nos clients mis à niveau la version la plus récente du produit de hello toohello. Par conséquent, nous avons dû toosupport plusieurs versions, rendre hello prend en charge également les toodo très difficile de travail. »

Été ajoute, « nous voulions une manière tooprogram et la version des mises à jour à une accélération du rythme, afin que nous avons innover plus rapidement et créer de nouveaux services pour nos clients. Nous avons également souhaité qu'un tooautomate de façon plus traite dans l’ordre toosimplify nos clients administration de l’entreprise. »

Pour SnelStart, hello solution a été tooextend ses services en devenant un fournisseur SaaS basée sur le cloud. plateforme de base de données SQL Azure Hello SnelStart permettait d’y accéder sans subir la surcharge informatique principales hello qui aurait requis une solution d’infrastructure-as-a-service (IaaS).

modèle de cloud Hello permet SnelStart toofix bogues également et fournit de nouvelles fonctionnalités rapidement, sans les clients nécessitant des toodownload et le logiciel de mise à niveau. TooBeen conséquente, « à l’aide des services cloud Azure permet d’act tooquickly lors de la modification des exigences de tiers. Au lieu de tooship un toothousands version nouvelle de clients, nous pouvons adapter les informations envoyées à partir de notre application de bureau toonew les formats requis par des tiers. »

## <a name="a-modern-company-with-traditional-roots"></a>Une société moderne aux racines traditionnelles
SnelStart est une entreprise moderne, agile et de haute technologie racines modeste rencontres too1964, au démarrage fondateurs de hello entreprise de hello en tant que fabricant de parties de midi. cœur Hello Hello entreprise de logiciel SnelStart a réellement démarré battre Bonjour années 1980, au cours de la prolifération de hello de PC hello. société de Hello avait besoin d’un logiciel de comptabilité toohello autre meilleures au moment de hello, il a donc fallu questions dans son propre mains. En 1982, société de hello créé foundation hello de ce que serait cesser de logiciel de comptabilité SnelStart. À partir du début de hello, les logiciels hello a été admirées sa simplicité et la vitesse, de hello éventuellement modifié le focus et entreprise elle-même réinventée sous, dans un éditeur de logiciels.

En 1995, SnelStart a publié sa première application de comptabilité pour Windows. application Hello, repose sur des bases de données Microsoft Visual Basic 1.0 et Microsoft Access a permis de croissance toomore de base client hello à 5 000 utilisateurs.

Aujourd’hui, SnelStart est l’un des principaux fournisseurs d’applications métier (LOB) et d’administration destinées aux petites et moyennes entreprises et entrepreneurs indépendants néerlandais. Comme Carlo Kuip, architecte de l’informatique, dit, « notre objectif est automation de 100 % tooprovide des services d’administration de l’entreprise pour nos clients ».

## <a name="optimizing-performance-and-cost-with-elastic-pools"></a>Optimisation des performances et des coûts avec les pools élastiques
SnelStart a été un précurseur de l’adoption des pools élastiques à grande échelle. Pools élastiques limite les coûts de la société hello et gérer plus efficacement les exigences de performances. En fonction de tooBeen, « à l’aide de pools élastiques, nous pouvons optimiser les performances en fonction des besoins de hello de nos clients, sans un approvisionnement. Si nous avions tooprovision selon les pics de charge, il serait très coûteux. Bonjour à la place, les ressources de tooshare option entre plusieurs bases de données de faible utilisation permet de toocreate une solution qui fonctionne bien et rentable. »

## <a name="azure-sql-databases-help-containerize-data-for-isolation-and-security"></a>Les bases de données Azure SQL Database aident à conteneuriser les données dans un objectif d’isolement et de sécurité
Base de données SQL Azure permet de SnelStart tooeasily et déplacer de façon transparente tooAzure de données d’entreprise-administration de clients locaux. Hello, base de données SQL Azure est un conteneur pratique qui fournit une isolation, une limite pour l’authentification, l’autorisation et fonctionnalités de sauvegarde et de restauration facile. Les bases de données représentent un modèle conceptuel bien adapté à l’administration des entreprises. TooCarlo conséquente Kuip, architecte de l’informatique, « éléments au sein de cette limite de conteneur contiennent des données sensibles qui sont cruciale tooa business et le stockage de ces éléments dans un conserve une base de données isolé leur protection. Nous pouvons gérer l’autorisation au niveau de base de données hello et même automatiser la gestion de hello et montée en puissance parallèle de ces bases de données sans nécessiter des administrateurs de base de données (DBA) sur le personnel. »

Azure SQL Data Warehouse joue également un rôle dans l’article de sécurité et la gestion de SnelStart hello en entreprise de hello permettant de collecter des données de télémétrie, telles que la détection d’intrusion, enregistrement de l’activité utilisateur et la connectivité.

## <a name="azure-removes-overhead-so-that-developers-can-spend-more-time-delivering-value"></a>Azure élimine la surcharge de sorte que les développeurs puissent passer plus de temps à apporter une valeur ajoutée
modèle de plateforme Windows Azure Hello supprimé des charges d’infrastructure et activé des déploiements de tooautomate SnelStart à l’aide des bibliothèques de gestion c#. Comme les États de Kuip, « nous avons toogrow en mesure de nos opérations en cours avec une très petite personnel pendant simultanément augmenter l’évolutivité, la vitesse et récupération d’urgence des options pour nos clients. développement de Hello MAJ tooservices libérées ressources toofocus de nouveaux services et fonctionnalités, au lieu de mettre à jour uniquement tookeep de code existant d’avec de nouveaux codes règlements ou fiscales. » Il ajoute « Par l’automatisation de la gestion et à l’aide de l’offre SaaS hello, nous sont en mesure de toodeliver plus de valeur pour nos clients sans avoir toomake importants investissements dans personnel ». Par exemple, à l’aide de pools élastiques et Azure, SnelStart a été en mesure de tooadd une variété de nouvelles fonctionnalités, y compris l’intégration de données des clients plus fiable avec des banques, nouvelle facturation des services, les contrôles en arrière-plan des petites entreprises et les services de messagerie.

> « Hello simplement premiers mois de 2016, nous avons développé notre déploiements de base de données SQL Azure à partir d’environ 5 500 toomore à 12 000, et nous ajoutons actuellement plus de 1 000 bases de données par mois. »
> 
> — Henry Been, architecte logiciel
> 
> 

En outre, gestion de la base de données est automatisée à l’aide de fonctionnalité de travaux élastique hello. Comme les États de Kuip, « hautement Merci pour la découverte automatique de bases de données sur une instance de base de données SQL [serveur] hello. » Cela permet de SnelStart tooexecute les opérations de gestion sur leurs clients dynamiquement en expansion base sans surcharge supplémentaire.

SnelStart développe également une API qui fonctionne comme un répartiteur entre les données des clients et les applications créées par les partenaires logiciels tiers. Comme les États Kuip, « cette API activera tooadd fonctionnalité tooour logiciel d’autres fournisseurs, par exemple en éliminant la saisie de données pour les factures et autres documents. » Les clients n’auront plus toomanually les factures de type dans leurs logiciels de Comptabilité PME ; Hello SnelStart logiciel échangent les informations nécessaires hello directement. Cela permet aux clients toojoin leur administration de l’entreprise des tâches avec l’écosystème hello d’informations découlant de transformation numérique dans le secteur de hello.  

## <a name="how-azure-services-enable-saas-for-snelstart"></a>Comment les services Azure donnent à SnelStart l’accès au SaaS
À l’aide de Azure, SnelStart peut servir de ses clients et leurs éprouve des difficultés plus en toute transparence dans le cloud de hello. Par exemple, les clients et les comptables peuvent partager des informations en accédant directement aux API clientes de SnelStart, hébergées sur Azure. Les États de Kuip, « ces services réutilisables sont les applications web côté client tooour disponibles et fournissent infrastructure commune et des fonctions administration de toobusiness tooallow accès pour les clients et les logiciels tiers toothird utilisés par nos clients. Ces fonctionnalités comprennent notamment la configuration des produits, la gestion des règles de pare-feu et la gestion des processus longs, comme les sauvegardes. »

> Notre objectif est automation de 100 % tooprovide des services d’administration de l’entreprise pour nos clients. » 
> 
> — Carlo Kuip, architecte informatique
> 
> 

En outre, des services web SnelStart autoriser les clients et accéder aux données de la tooeasily éprouve des difficultés dans les pools élastiques de base de données SQL Azure. Ce modèle SaaS, associé à l’élasticité des bases de données et à Azure Resource Manager, offre à SnelStart des fonctionnalités d’évolutivité qui complètent chaque déploiement Azure. implémentation de Hello est entièrement automatisée à l’aide des bibliothèques de gestion c#.

![Architecture SnelStart](./media/sql-database-implementation-snelstart/figure1.png)

Figure 1. En juin 2016, SnelStart avait plus de 11 000 bases de données et plus de 50 pools élastiques

## <a name="simplicity-from-hello-cloud"></a>Simplicité du cloud de hello
Le mouvement tooan solution basée sur le cloud sur Azure, SnelStart a été toosupport en mesure de la croissance rapide de client tout en offrant des services et fonctionnalités innovantes. En fonction de tooBeen, « avec Azure, nous pouvons fournir quasi continue mises à jour pour nos clients, sans développer notre personnel chargé des opérations. Et nous obtenons hello toutes les autres fonctionnalités d’Azure, telles que l’évolutivité et récupération d’urgence, regroupés dans. »

> « Lorsque nous ont été réellement au cours de Redmond... J’ai reçu un appel à partir d’un développeur dans hello pays-bas, m’appelant sur un problème spécifique. Nous ont été en mesure de tooget Microsoft toodeliver une modification de leur environnement de production dans les dernières 48 heures toosolve notre problème. »
> 
> — Henry Been, architecte logiciel
> 
> 

SnelStart remercie également hello solide partenariat que leur avez développé avec l’équipe de base de données SQL Microsoft Azure hello. En tant que les États Kuip, « nous avons des discussions sur les fonctionnalités et comment la technologie toouse, qui est un élément appréciée des deux côtés. »
Hello immédiate SnelStart vise tookeep augmente la base de son client satisfait. Comme été États, « Sans hello technique et les limitations de ressources que nous avons dû en tant qu’ISV, il n’existe aucun toohow limite présent nous permet de développer. »

## <a name="more-information"></a>Plus d’informations
* toolearn en savoir plus sur les pools élastiques Azure, consultez [pools élastiques](sql-database-elastic-pool.md).
* toolearn en savoir plus sur les rôles Web et worker, consultez [rôles de travail](../fundamentals-introduction-to-azure.md#compute).    
* toolearn savoir plus sur l’entrepôt de données SQL Azure, consultez [SQL Data Warehouse](https://azure.microsoft.com/documentation/services/sql-data-warehouse/)
* toolearn en savoir plus sur SnelStart, consultez [SnelStart](http://www.snelstart.nl).

