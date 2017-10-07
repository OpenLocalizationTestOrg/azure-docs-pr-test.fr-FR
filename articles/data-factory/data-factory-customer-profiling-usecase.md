---
title: aaaUse cas - client de profilage
description: "Découvrez comment Azure Data Factory est utilisé toocreate piloté par des données du flux de travail (pipeline) tooprofile jeu clients."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: e07d55cf-8051-4203-9966-bdfa1035104b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 47f5e77242366c80cce2a2db65e3c696505b3e1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-case---customer-profiling"></a>Cas d’utilisation - Profilage des utilisateurs
Azure Data Factory est un des nombreux services utilisés de tooimplement hello Cortana Intelligence Suite d’accélérateurs de solutions.  Pour plus d’informations sur Cortana Intelligence, consultez [Cortana Intelligence Suite](http://www.microsoft.com/cortanaanalytics). Dans ce document, nous décrivons une toohelp de cas d’utilisation simples comment commencer à comprendre comment Azure Data Factory peut résoudre les problèmes courants analytique.

## <a name="scenario"></a>Scénario
Contoso est une société qui crée des jeux pour plusieurs plateformes : des consoles de jeux, des appareils portatifs et des ordinateurs personnels (PC). Comme les lecteurs de lire ces jeux, gros volume de données de journal est généré que pistes hello des modèles d’utilisation, le style de jeux et les préférences de l’utilisateur de hello.  Lorsque vous associez des données démographiques, régionales, et les données de produit, Contoso peut effectuer tooguide analytique elles sur comment joueurs tooenhance rencontrer et ciblent les mises à niveau et de la partie achats. 

Objectif de Contoso est tooidentify up-donneur d’ordre/des opportunités de vente en fonction de l’historique des jeux hello de ses lecteurs et ajouter des fonctionnalités toodrive gestion de la croissance et fournir une meilleure toocustomers d’expérience. Pour ce cas d’utilisation, nous prenons l’exemple d’un développeur de jeux. société de Hello veut toooptimize ses jeux basés sur le comportement des joueurs. Ces principes s’appliquent tooany entreprise qui veut tooengage ses clients autour de ses produits et les services et amélioreront l’expérience de leurs clients.

Dans cette solution, Contoso souhaite que l’efficacité de hello tooevaluate d’une campagne marketing, qu'il a récemment lancé. Nous démarrer avec des journaux de jeu brut hello, processus enrichir les données de géolocalisation joindre à la publication des données de référence et, enfin, copiez-les dans l’impact d’une base de données SQL Azure tooanalyze hello la campagne.

## <a name="deploy-solution"></a>Déployer la solution
Tous les vous devez tooaccess et essayer de ce cas de figure simple est un [abonnement Azure](https://azure.microsoft.com/pricing/free-trial/), un [compte de stockage d’objets Blob Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)et un [base de données SQL Azure](../sql-database/sql-database-get-started.md). Déploiement de client hello profilage pipeline à partir de hello **exemple pipelines** vignette sur la page d’accueil hello votre fabrique de données.

1. Créez une fabrique de données ou ouvrez une fabrique de données existante. Consultez [copier les données de stockage d’objets Blob tooSQL de base de données à l’aide de la fabrique de données](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour les étapes toocreate une fabrique de données.
2. Bonjour **DATA FACTORY** Panneau de fabrique de données hello, cliquez sur hello **exemple pipelines** vignette.

    ![Vignette Exemples de pipelines](./media/data-factory-samples/SamplePipelinesTile.png)
3. Bonjour **exemple pipelines** panneau, cliquez sur hello **client profilage** que vous souhaitez toodeploy.

    ![Panneau Exemples de pipelines](./media/data-factory-samples/SampleTile.png)
4. Spécifiez les paramètres de configuration de l’exemple hello. Par exemple, votre clé et votre nom de compte de stockage Azure, le nom du serveur SQL Azure, la base de données, l’ID d’utilisateur, le mot de passe.

    ![Panneau Exemple](./media/data-factory-samples/SampleBlade.png)
5. Une fois que vous avez terminé avec la spécification des paramètres de configuration hello, cliquez sur **créer** toocreate/déployer hello exemple pipelines et utilisés par les pipelines hello services/tables liées.
6. Vous consultez État hello de déploiement sur la vignette d’exemple hello vous avez cliqué précédemment sur hello **exemple pipelines** panneau.

    ![état du déploiement](./media/data-factory-samples/DeploymentStatus.png)
7. Lorsque vous consultez hello **déploiement a réussi** message sur la vignette hello pour exemple hello, fermer hello **exemple pipelines** panneau.  
8. Sur **DATA FACTORY** panneau, vous voyez que les services liés, les jeux de données et les pipelines sont ajoutés fabrique de données tooyour.  

    ![Panneau Data Factory](./media/data-factory-samples/DataFactoryBladeAfter.png)

## <a name="solution-overview"></a>Vue d’ensemble de la solution
Cette case d’utilisation simple peut être utilisé comme un exemple de la façon dont vous pouvez utiliser Azure Data Factory tooingest, préparer, transformer, analyser et publier des données.

![Workflow de bout en bout](./media/data-factory-customer-profiling-usecase/EndToEndWorkflow.png)

Cette Figure illustre comment hello des pipelines de données s’affichent dans hello portail Azure une fois qu’ils ont été déployés.

1. Hello **PartitionGameLogsPipeline** lit les événements de jeu bruts hello depuis le stockage blob et crée des partitions basées sur l’année, mois et jour.
2. Hello **EnrichGameLogsPipeline** joint des événements de jeu partitionnées avec les données de référence de code de géo-réplication et enrichit les données de hello en mappant IP adresses toohello correspondantes emplacements géographiques.
3. Hello **AnalyzeMarketingCampaignPipeline** pipeline utilise hello enrichie des données et le traite avec hello publicité données toocreate hello finale qui contient l’efficacité de la campagne marketing.

Dans cet exemple, la fabrique de données est tooorchestrate utilisé les activités qui copie les données d’entrée, de transformation et de traiter les données hello et sortie hello finale des données tooan base de données SQL Azure.  Vous pouvez également visualiser réseau hello des pipelines de données, les gérer et surveiller leur état à partir de l’interface utilisateur de hello.

## <a name="benefits"></a>Avantages
En optimisant leur analytique de profil utilisateur et les aligner avec les objectifs, société de jeu est en mesure de tooquickly des modèles d’utilisation de collecter et analyser l’efficacité de ses campagnes marketing hello.

