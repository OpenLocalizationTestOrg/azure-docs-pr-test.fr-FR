---
title: aaaUse un local SQL Server dans Azure Machine Learning | Documents Microsoft
description: "Utiliser des données à partir d’un analytique de tooperform avancé de base de données SQL Server local avec Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 08e4610d-02b6-4071-aad7-a2340ad8e2ea
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: garye;krishnan
ms.openlocfilehash: c0e9908e296b97b31611ef0192744a59073acd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="perform-advanced-analytics-with-azure-machine-learning-using-data-from-an-on-premises-sql-server-database"></a>Effectuer des analyses avancées avec Azure Machine Learning en utilisant les données d’une base de données SQL Server locale

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

Fréquence à laquelle les entreprises qui fonctionnent avec des données locales aimeriez parti tootake de montée en puissance hello et l’agilité de cloud hello pour leur charges de travail d’apprentissage. Mais ils ne souhaitent pas toodisrupt leurs processus d’entreprise en cours et le flux de travail en déplaçant leur cloud toohello de données local. Azure Machine Learning prend désormais en charge la lecture de vos données à partir d’une base de données SQL Server locale, puis l’apprentissage et l’évaluation d’un modèle avec ces données. Vous n’avez plus toomanually copier et synchronisation hello des données entre le cloud de hello et de votre serveur local. Au lieu de cela, hello **importer des données** module dans Azure Machine Learning Studio peut désormais lire directement à partir de votre base de données SQL Server locale pour votre apprentissage et le score des travaux.

Cet article fournit une vue d’ensemble du mode tooingress local de données SQL server dans Azure Machine Learning. Il part du principe que vous êtes familiarisé avec les concepts d’Azure Machine Learning, comme les espaces de travail, les modules, les jeux de données, les expériences, *etc*.

> [!NOTE]
> Cette fonctionnalité n’est pas disponible pour les espaces de travail gratuits. Pour plus d’informations sur la tarification et les niveaux de Machine Learning, consultez la [Tarification d’Azure Machine Learning](https://azure.microsoft.com/pricing/details/machine-learning/).
>
>

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="install-hello-microsoft-data-management-gateway"></a>Installer hello passerelle de gestion des données Microsoft
tooaccess une base de données SQL Server locale dans Azure Machine Learning, vous devez toodownload et installation hello passerelle de gestion des données de Microsoft. Lorsque vous configurez la connexion à la passerelle hello dans Machine Learning Studio, vous avez opportunité hello pour télécharger et installer la passerelle hello à l’aide de hello **téléchargement et la passerelle de données de Registre** boîte de dialogue décrite ci-dessous.

Vous pouvez également installer hello passerelle de gestion des données avance en téléchargeant et en exécutant le package d’installation MSI hello de hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).
Choisissez la version la plus récente hello, en sélectionnant 32 bits ou 64 bits en fonction de votre ordinateur. Hello MSI peut également être utilisé tooupgrade une passerelle de gestion des données toohello dernière version existante, avec tous les paramètres sont conservés.

passerelle de Hello a hello suivant des conditions préalables :

* versions de système d’exploitation Windows Hello pris en charge sont Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012 et Windows Server 2012 R2.
* Hello recommandé de configuration pour l’ordinateur de passerelle hello est au moins 2 GHz, 4 cœurs, 8 Go de RAM et disque de 80 Go.
* Si l’ordinateur hôte de hello en veille prolongée, passerelle de hello ne répondra toodata demandes. Par conséquent, configurez un plan d’alimentation sur l’ordinateur de hello avant d’installer la passerelle de hello. Si la machine de hello est toohibernate configuré, installation de la passerelle hello affiche un message.
* Étant donné que l’activité de copie se produit à une fréquence spécifique, hello l’utilisation des ressources (processeur, mémoire) sur l’ordinateur de hello suit également hello même modèle avec des heures de pointe et les temps d’inactivité. L’utilisation des ressources également dépend fortement hello quantité de données en cours de déplacement. Quand plusieurs travaux de copie sont en cours, vous constaterez une augmentation des ressources utilisées pendant les heures de pointe. Alors que la configuration minimale hello répertoriée ci-dessus est techniquement suffisante, vous souhaiterez toohave une configuration avec plus de ressources que la configuration minimale hello en fonction de votre charge spécifique pour le déplacement des données.

Considérez les éléments hello lors de la configuration et l’utilisation d’une passerelle de gestion des données suivants :

* Vous ne pouvez installer qu’une seule instance de la passerelle de gestion des données sur un même ordinateur.
* Vous pouvez utiliser une seule passerelle pour plusieurs sources de données locales.
* Vous pouvez vous connecter à plusieurs passerelles sur différents ordinateurs toohello même source de données locale.
* Vous ne configurez une passerelle que pour un seul espace de travail à la fois. Pour le moment, les passerelles ne peuvent pas être partagées entre plusieurs espaces de travail.
* Vous pouvez configurer plusieurs passerelles pour un espace de travail unique. Par exemple, vous voudrez toouse une passerelle est connectée tooyour des sources de données de test pendant le développement et une passerelle de production quand vous êtes prêt toooperationalize.
* passerelle de Hello n’a pas besoin toobe sur hello même ordinateur en tant que source de données hello. Mais rester proche toohello source de données réduit le temps de hello pour la source de données hello passerelle tooconnect toohello. Nous vous recommandons d’installer la passerelle de hello sur un ordinateur qui est différent de hello une source de données hôtes hello local afin que hello passerelle et source de données ne sont en concurrence pour les ressources.
* Si une passerelle est déjà installée sur votre ordinateur desservant des scénarios Power BI ou Azure Data Factory, installez une passerelle distincte pour Azure Machine Learning sur un autre ordinateur.

  > [!NOTE]
  > Vous ne pouvez pas exécuter passerelle de gestion des données et Power BI Gateway sur hello même ordinateur.
  >
  >
* Vous devez toouse hello passerelle de gestion des données pour Azure Machine Learning, même si vous utilisez Azure ExpressRoute pour d’autres données. Traitez votre source de données comme une source de données locale (derrière un pare-feu), même quand vous utilisez ExpressRoute. Utiliser une connexion de tooestablish hello passerelle de gestion des données entre l’apprentissage et de la source de données hello.

Vous trouverez des informations détaillées sur les conditions préalables d’installation, des étapes d’installation et des conseils de dépannage dans l’article de hello [passerelle de gestion des données](../data-factory/data-factory-data-management-gateway.md).

## <a name="span-idusing-the-data-gateway-step-by-step-walk-classanchorspan-idtoc450838866-classanchorspanspaningress-data-from-your-on-premises-sql-server-database-into-azure-machine-learning"></a><span id="using-the-data-gateway-step-by-step-walk" class="anchor"><span id="_Toc450838866" class="anchor"></span></span>Intégrer des données de votre base de données SQL Server locale dans Azure Machine Learning
Dans cette procédure pas à pas, vous allez configurer une passerelle de gestion des données dans un espace de travail Azure Machine Learning, la configurer, puis lire les données à partir d’une base de données SQL Server locale.

> [!TIP]
> Avant de commencer, désactivez le bloqueur de fenêtres publicitaires de votre navigateur pour `studio.azureml.net`. Si vous utilisez hello navigateur Google Chrome, télécharger et installer l’une de hello plusieurs plug-ins disponibles à Google Chrome WebStore [Extension d’application une fois cliquez sur](https://chrome.google.com/webstore/search/clickonce?_category=extensions).
>
>

### <a name="step-1-create-a-gateway"></a>Étape 1 : Créer une passerelle
première étape de Hello est toocreate et configurez hello passerelle tooaccess de votre base de données SQL locale.

1. Connectez-vous trop[Azure Machine Learning Studio](https://studio.azureml.net/Home/) et sélectionnez hello espace de travail toowork dans.
2. Cliquez sur hello **paramètres** panneau sur hello gauche, puis cliquez sur hello **passerelles de données** onglet en haut de hello.
3. Cliquez sur **nouvelle passerelle de données** bas hello écran hello.

    ![Nouvelle passerelle de données](media/machine-learning-use-data-from-an-on-premises-sql-server/new-data-gateway-button.png)
4. Bonjour **nouvelle passerelle de données** boîte de dialogue, entrez hello **nom de la passerelle** et ajoutez éventuellement un **Description**. Cliquez sur flèche hello sur hello en bas à droite toogo toohello étape suivante de la configuration de hello.

    ![Entrez la description et le nom de la passerelle](media/machine-learning-use-data-from-an-on-premises-sql-server/new-data-gateway-dialog-enter-name.png)
5. Bonjour, télécharger et enregistrer la boîte de dialogue de la passerelle de données, copier le Presse-papiers toohello clé d’inscription de passerelle hello.

    ![Téléchargez et enregistrez la passerelle de données](media/machine-learning-use-data-from-an-on-premises-sql-server/download-and-register-data-gateway.png)
6. <span id="note-1" class="anchor"></span>Si vous n’avez pas encore téléchargé et installé hello passerelle de gestion des données de Microsoft, puis cliquez sur **passerelle de gestion des données téléchargement**. Cette prend toothe Microsoft Download Center où vous pouvez sélectionner la version de la passerelle hello vous avez besoin, téléchargez-le et installez-le. Vous trouverez des informations détaillées sur les conditions préalables d’installation, des étapes d’installation et des conseils de dépannage dans hello premières sections de l’article de hello [déplacement des données entre des sources locales et cloud avec la passerelle de gestion des données](../data-factory/data-factory-move-data-between-onprem-and-cloud.md).
7. Après l’installation de la passerelle de hello, hello Gestionnaire de Configuration de passerelle de gestion de données s’ouvre et hello **Registre passerelle** boîte de dialogue s’affiche. Hello de coller **clé d’inscription de passerelle** que vous avez copié toohello Presse-papiers, puis cliquez sur **inscrire**.
8. Si vous disposez déjà d’une passerelle installée, exécutez hello Gestionnaire de Configuration de passerelle de gestion de données. Cliquez sur **modifier la clé**, collez la **clé d’inscription de passerelle** que vous avez copié toohello Presse-papiers dans l’étape précédente de hello, puis cliquez sur **OK**.
9. Lors de l’installation de hello est terminée, hello **Registre passerelle** boîte de dialogue pour le Gestionnaire de Configuration de passerelle Microsoft Data Management s’affiche. Collez hello clé d’inscription de passerelle que vous avez copié dans le Presse-papiers hello à l’étape précédente, puis cliquez sur **inscrire**.

    ![Inscrivez la passerelle](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-register-gateway.png)
10. Hello configuration de la passerelle est terminée lorsque hello valeurs suivantes est définie sur hello **accueil** onglet dans le Gestionnaire de Configuration de passerelle Microsoft Data Management :

    * **Nom de la passerelle** et **nom de l’Instance** sont définies nom toohello de passerelle de hello.
    * **L’enregistrement** est défini trop**inscrit**.
    * **État** est défini trop**démarré**.
    * barre d’état de Hello en hello bas affiche **connecté tooData Service de Cloud de passerelle de gestion** avec une coche verte.

      ![Gestionnaire de passerelle de gestion de données](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-registered.png)

      Azure Machine Learning Studio est actualisée lors de l’inscription de hello a réussi.

    ![Inscription de la passerelle réussie](media/machine-learning-use-data-from-an-on-premises-sql-server/gateway-registered.png)
11. Bonjour **télécharger et inscrire la passerelle de données** boîte de dialogue, cliquez sur le programme d’installation de case à cocher toocomplete hello. Hello **paramètres** page affiche l’état de la passerelle comme étant « En ligne ». Vous trouverez dans le volet de droite hello, état et autres informations utiles.

    ![Paramètres de la passerelle](media/machine-learning-use-data-from-an-on-premises-sql-server/gateway-status.png)
12. Dans le Gestionnaire de Configuration de passerelle de gestion de données de Microsoft de hello basculer toohello **certificat** certificat de hello onglet spécifiée sous cet onglet est utilisé tooencrypt/déchiffrer les informations d’identification pour la banque de données locale hello que vous spécifiez dans le portail de hello. Ce certificat est un certificat par défaut de hello. Microsoft vous recommande de modification de ce certificat propre tooyour que vous sauvegardez dans votre système de gestion de certificat. Cliquez sur **modification** toouse votre propre certificat à la place.

    ![Changez le certificat de la passerelle](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-certificate.png)
13. (facultatif) Si vous souhaitez que la journalisation documentée de tooenable afin de résoudre les problèmes avec la passerelle de hello, dans le Gestionnaire de Configuration de passerelle de gestion de données de Microsoft de hello basculer toothe **Diagnostics** et vérifiez hello **activer la journalisation à des fins de dépannage détaillée** option. Hello des informations de journalisation sont accessibles dans hello Observateur d’événements Windows sous hello **journaux des Applications et Services**  - &gt; **passerelle de gestion des données** nœud. Vous pouvez également utiliser hello **Diagnostics** onglet tootest hello connexion tooan local source de données à l’aide de la passerelle de hello.

    ![Activez la journalisation commentée](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-verbose-logging.png)

Cette étape termine le processus de configuration de passerelle hello dans Azure Machine Learning.
Vous êtes maintenant prêt toouse vos données locales.

Vous pouvez créer et configurer plusieurs passerelles dans Studio pour chaque espace de travail. Par exemple, peut avoir une passerelle que vous souhaitez les sources de données de test tooconnect tooyour pendant le développement et une autre passerelle pour vos sources de données de production. Azure Machine Learning vous donne la souplesse tooset des passerelles multiples en fonction de votre environnement d’entreprise. Actuellement, vous ne pouvez pas partager une passerelle entre différents espaces de travail et une seule passerelle peut être installée sur un même ordinateur. Pour plus d’informations, consultez [Déplacement de données entre des sources locales et le cloud à l’aide de la passerelle de gestion des données](../data-factory/data-factory-move-data-between-onprem-and-cloud.md).

### <a name="step-2-use-hello-gateway-tooread-data-from-an-on-premises-data-source"></a>Étape 2 : Utiliser hello passerelle tooread les données à partir d’une source de données locale
Après avoir configuré la passerelle de hello, vous pouvez ajouter un **importer des données** module pour une expérience qui entre des données hello à partir de la base de données SQL Server de hello locale.

1. Dans la Machine Learning Studio, sélectionnez hello **expériences** , cliquez sur **+ nouveau** dans hello coin inférieur gauche, puis sélectionnez **expérience vide** (ou sélectionnez un des exemples de plusieurs expériences disponibles).
2. Rechercher et faites glisser hello **importer des données** module toohello expérimenter la zone de dessin.
3. Cliquez sur **enregistrer en tant que** sous la zone de dessin hello. Entrez « Azure Machine Learning local SQL Server didacticiel » pour le nom d’expérience hello, sélectionnez l’espace de travail, cliquez sur hello **OK** case à cocher.

   ![Enregistrez l’expérience sous un nouveau nom](media/machine-learning-use-data-from-an-on-premises-sql-server/experiment-save-as.png)
4. Cliquez sur hello **importer des données** tooselect de module, puis dans le **propriétés** toohello volet à droite de la zone de dessin hello, sélectionnez « Base de données locale SQL » Bonjour **source de données** liste déroulante.
5. Sélectionnez hello **passerelle de données** vous avez installé et enregistré. Vous pouvez configurer une autre passerelle en sélectionnant « (ajouter une nouvelle passerelle de données...) ».

   ![Sélectionnez une passerelle de données pour le module d’importation de données](media/machine-learning-use-data-from-an-on-premises-sql-server/import-data-select-on-premises-data-source.png)
6. Entrez hello SQL **nom du serveur de base de données** et **nom de la base de données**, ainsi que de hello SQL **requête de base de données** vous souhaitez tooexecute.
7. Cliquez sur **Entrer des valeurs** sous **Nom d’utilisateur et mot de passe** et entrez vos informations d’identification de base de données. Vous pouvez utiliser l’authentification intégrée Windows ou l’authentification SQL Server en fonction de la configuration de votre serveur local SQL Server.

   ![Entrez les informations d’identification de la base de données](media/machine-learning-use-data-from-an-on-premises-sql-server/database-credentials.png)

   message de type Hello les modifications « valeurs requises » trop « valeur » avec une coche verte. Il vous suffit d’informations d’identification de tooenter hello qu’une seule fois, sauf si les informations de base de données hello ou le mot de passe change. Azure Machine Learning utilise un certificat hello que vous avez fourni lorsque vous avez installé des informations d’identification de hello passerelle tooencrypt hello dans le cloud de hello. Azure ne stocke jamais d’informations d’identification locales sans chiffrement.

   ![Importez les propriétés du module de données](media/machine-learning-use-data-from-an-on-premises-sql-server/import-data-properties-entered.png)
8. Cliquez sur **exécuter** expérience de hello toorun.

Une fois que l’expérience de hello a terminé son exécution, vous pouvez visualiser les données de hello vous avez importé à partir de la base de données hello en cliquant sur le port de sortie hello Hello **importer des données** module et en sélectionnant **visualiser**.

Une fois que vous avez terminé le développement de votre expérience, vous pouvez déployer et opérationnaliser votre modèle. À l’aide de hello Batch Execution Service, les données de base de SQL Server locale hello configuré Bonjour **importer des données** module est lus et utilisé pour calculer les scores. Vous pouvez utiliser hello demander un Service de réponse pour calculer les scores des données localement, Microsoft recommande d’utiliser le [complément Excel](machine-learning-excel-add-in-for-web-services.md) à la place. Actuellement, l’écriture tooan local de la base de données SQL Server via **exporter les données** n’est pas les services web en soit vos expériences ou publiées.
