---
title: "aaaCustomize Hadoop clusters pour hello processus de science des données équipe | Documents Microsoft"
description: "Modules de Python populaires disponibles dans les clusters Hadoop Azure HDInsight personnalisés."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0c115dca-2565-4e7a-9536-6002af5c786a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: e192542dd39f71bccbb5163382b4050d0f12ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-azure-hdinsight-hadoop-clusters-for-hello-team-data-science-process"></a>Personnaliser les clusters Azure HDInsight Hadoop pour hello processus de science des données équipe
Cet article décrit comment toocustomize un HDInsight Hadoop de cluster en installant 64 bits Anaconda (Python 2.7) sur chaque nœud lorsque le cluster de hello est approvisionné comme un service HDInsight. Il montre également comment tooaccess hello cluster toohello de nœud principal toosubmit des tâches personnalisées. Cette personnalisation permet de nombreux modules Python populaires, qui sont inclus dans Anaconda, facilement disponibles pour une utilisation dans utilisateur défini les fonctions qui sont conçues tooprocess enregistrements Hive dans le cluster de hello. Pour obtenir des instructions sur les procédures de hello utilisées dans ce scénario, consultez [comment les requêtes Hive toosubmit](machine-learning-data-science-move-hive-tables.md#submit).

Hello menu suivant lie tootopics qui décrivent comment tooset des hello différents environnements de science des données utilisé par hello [processus de science des données équipe (TDSP)](data-science-process-overview.md).

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

## <a name="customize"></a>Personnaliser le cluster Hadoop Azure HDInsight
toocreate un cluster HDInsight Hadoop personnalisé, commencez par session trop[**portail Azure classic**](https://manage.windowsazure.com/), cliquez sur **nouveau** à gauche de hello coin inférieur, puis sélectionnez les SERVICES de données -> HDINSIGHT -> **création personnalisée** toobring des hello **détails du Cluster** fenêtre. 

![Create workspace](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

Nom hello de hello toobe de cluster créé sur la page 1 de la configuration d’entrée et acceptez les valeurs par défaut pour hello autres champs. Cliquez sur toohello-page de configuration suivante hello flèche toogo. 

![Create workspace](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

Sur la page de configuration 2, entrez le nombre de hello de **nœuds de données**, sélectionnez hello **région/réseau virtuel**, puis sélectionnez les tailles de hello Hello **le nœud principal** et hello **Nœud de données**. Cliquez sur toohello-page de configuration suivante hello flèche toogo.

> [!NOTE]
> Hello **région/réseau virtuel** a toobe hello même région hello hello du compte de stockage qui est en train de toobe utilisé pour hello cluster HDInsight Hadoop. Sinon, dans la page configuration de la quatrième hello, compte de stockage hello apparaîtra pas dans la liste déroulante de hello des **nom de compte**.
> 
> 

![Create workspace](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img3.png)

Sur la page de configuration 3, fournissez un nom d’utilisateur et un mot de passe pour hello cluster HDInsight Hadoop. **Ne le faites pas** hello sélectionnez *entrée hello Metastores Hive/Oozie*. Ensuite, cliquez sur toohello-page de configuration suivante hello flèche toogo. 

![Create workspace](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img4.png)

Sur la page de configuration 4, spécifiez le nom de compte de stockage hello, conteneur par défaut de hello Hello cluster HDInsight Hadoop. Si vous sélectionnez *créer un conteneur par défaut* Bonjour **conteneur par défaut** liste déroulante, un conteneur avec hello même nom que celui que hello cluster sera créé. Cliquez sur hello flèche toogo toohello dernière configuration page.

![Create workspace](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img5.png)

Sur hello final **Actions de Script** page de configuration, cliquez sur **ajouter une action de script** bouton et remplissez les champs de texte hello avec hello valeurs suivantes.

* **NOM** -n’importe quelle chaîne comme nom hello de cette action de script
* **TYPE DE NŒUD** : sélectionnez **Tous les nœuds**
* **URI DE SCRIPT** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1* 
  * *publicscripts* est un conteneur public dans le compte de stockage hello 
  * *getgoing* nous utilisons tooshare PowerShell script fichiers toofacilitate travail des utilisateurs dans Azure
* **PARAMÈTRES** : (laisser cette zone vide)

Enfin, cliquez sur hello coche toostart hello la création de cluster HDInsight Hadoop de hello personnalisé. 

![Create workspace](./media/machine-learning-data-science-customize-hadoop-cluster/script-actions.png)

## <a name="headnode"></a>Accéder au nœud principal de Hadoop Cluster de hello
Vous devez activer le cluster de Hadoop toohello l’accès à distance dans Azure avant de pouvoir accéder hello nœud de tête hello Hadoop cluster via RDP. 

1. Connectez-vous à toohello [ **portail Azure classic**](https://manage.windowsazure.com/), sélectionnez **HDInsight** sur hello gauche, sélectionnez votre cluster Hadoop dans liste hello de clusters, cliquez sur hello  **CONFIGURATION** onglet, puis cliquez sur hello **activer distant** icône bas hello de page de hello.
   
    ![Create workspace](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-1.png)
2. Bonjour **configurer le Bureau à distance** fenêtre, entrez hello nom d’utilisateur et les champs de mot de passe et sélectionnez la date d’expiration de hello pour l’accès à distance. Cliquez ensuite sur hello coche tooenable hello accès à distance toohello nœud principal du cluster Hadoop de hello.
   
    ![Create workspace](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-2.png)

> [!NOTE]
> nom d’utilisateur Hello et le mot de passe pour l’accès à distance hello ne sont pas nom d’utilisateur hello et un mot de passe que vous utilisez lorsque vous avez créé le cluster Hadoop de hello. Il s’agit d’un ensemble d’informations d’identification distinct. En outre, date d’expiration de hello d’accès à distance de hello a toobe dans les 7 jours à partir de hello date actuelle.
> 
> 

Une fois l’accès à distance est activé, cliquez sur **CONNECT** bas hello tooremote de page hello dans le nœud principal de hello. Vous ouvrez une session toohello le nœud principal du cluster Hadoop de hello en entrant les informations d’identification hello pour l’utilisateur de l’accès à distance hello que vous avez spécifié précédemment.

![Create workspace](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-3.png)

les étapes suivantes dans hello avancé du processus d’analytique Hello sont mappées dans hello [processus de science des données équipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) et peuvent inclure des étapes de déplacement des données dans HDInsight, puis traitent et aperçu en préparation pour l’apprentissage à partir des données de hello avec Azure Machine Learning.

Consultez [comment les requêtes Hive toosubmit](machine-learning-data-science-move-hive-tables.md#submit) pour obtenir des instructions sur la façon dont tooaccess hello modules Python inclus dans Anaconda à partir du nœud principal de hello du cluster hello dans les fonctions utilisateur (UDF) qui sont utilisés tooprocess Hive enregistrements stockés dans un cluster de hello.

