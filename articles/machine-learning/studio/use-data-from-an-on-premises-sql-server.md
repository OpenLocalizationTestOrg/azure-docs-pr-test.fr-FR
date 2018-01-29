---
title: Utiliser un serveur SQL Server local dans Azure Machine Learning | Microsoft Docs
description: "Utilisez les données d’une base de données SQL Server locale pour effectuer des analyses avancées avec Azure Machine Learning."
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
ms.openlocfilehash: 79ae5cd78ce07fcc84be49c2693773d58a15771e
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="perform-advanced-analytics-with-azure-machine-learning-using-data-from-an-on-premises-sql-server-database"></a>Effectuer des analyses avancées avec Azure Machine Learning en utilisant les données d’une base de données SQL Server locale

[!INCLUDE [import-data-into-aml-studio-selector](../../../includes/machine-learning-import-data-into-aml-studio.md)]

Souvent, les entreprises qui travaillent avec des données locales souhaitent tirer parti de l’échelle et de l’agilité du cloud pour leurs charges de travail d’apprentissage automatique. Mais elles ne souhaitent pas perturber leurs processus métier et leurs flux de travail actuels en déplaçant leurs données locales vers le cloud. Azure Machine Learning prend désormais en charge la lecture de vos données à partir d’une base de données SQL Server locale, puis l’apprentissage et l’évaluation d’un modèle avec ces données. Vous n’avez plus à copier et à synchroniser manuellement les données entre le cloud et votre serveur local. Au lieu de cela, le module **Importer des données** dans Azure Machine Learning Studio peut maintenant lire directement dans votre base de données SQL Server locale pour vos travaux d’apprentissage et d’évaluation.

Cet article fournit une vue d’ensemble de l’intégration de données SQL Server locales dans Azure Machine Learning. Il part du principe que vous êtes familiarisé avec les concepts d’Azure Machine Learning, comme les espaces de travail, les modules, les jeux de données, les expériences, *etc*.

> [!NOTE]
> Cette fonctionnalité n’est pas disponible pour les espaces de travail gratuits. Pour plus d’informations sur la tarification et les niveaux de Machine Learning, consultez la [Tarification d’Azure Machine Learning](https://azure.microsoft.com/pricing/details/machine-learning/).
>
>

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../../includes/machine-learning-free-trial.md)]

## <a name="install-the-microsoft-data-management-gateway"></a>Installer la passerelle de gestion des données de Microsoft
Pour accéder à une base de données SQL Server locale dans Azure Machine Learning, vous devez télécharger et installer la passerelle de gestion des données de Microsoft. Quand vous configurez la connexion de passerelle dans Machine Learning Studio, vous avez la possibilité de télécharger et d’installer la passerelle à l’aide de la boîte de dialogue **Télécharger et inscrire la passerelle de données** décrite ci-dessous.

Vous pouvez également installer la passerelle de gestion des données à l’avance en téléchargeant et en exécutant le package d’installation MSI dans le [Centre de téléchargement Microsoft](https://www.microsoft.com/download/details.aspx?id=39717).
Choisissez la version la plus récente, en sélectionnant 32 bits ou 64 bits en fonction de votre ordinateur. Le fichier MSI peut également servir à mettre à niveau une passerelle de gestion des données existante vers la version la plus récente, en conservant tous les paramètres.

La passerelle nécessite les éléments suivants :

* Les versions de système d’exploitation Windows prises en charge sont les suivantes : Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012 et Windows Server 2012 R2.
* La configuration recommandée pour l’ordinateur de passerelle est la suivante : au moins 2 GHz, 4 cœurs, 8 Go de RAM et 80 Go d’espace disque.
* Si l’ordinateur hôte est en veille prolongée, la passerelle ne répond pas aux demandes de données. Vous devez donc configurer un plan de gestion de l'alimentation approprié sur l'ordinateur avant d'installer la passerelle. Si l’ordinateur est configuré pour se mettre en veille prolongée, l’installation de la passerelle affiche un message.
* Étant donné que l’activité de copie se déroule selon une fréquence spécifique, l’utilisation des ressources (processeur, mémoire) sur l’ordinateur suit également le même modèle avec des périodes de pointe et d’inactivité. L'utilisation des ressources dépend également en grande partie de la quantité de données déplacées. Quand plusieurs travaux de copie sont en cours, vous constaterez une augmentation des ressources utilisées pendant les heures de pointe. Si la configuration minimale listée ci-dessus est techniquement suffisante, vous pouvez choisir d’avoir une configuration avec plus de ressources que la configuration minimale en fonction de votre charge spécifique pour le déplacement des données.

Prenez en compte ce qui suit lors de la configuration et de l’utilisation d’une passerelle de gestion des données :

* Vous ne pouvez installer qu’une seule instance de la passerelle de gestion des données sur un même ordinateur.
* Vous pouvez utiliser une seule passerelle pour plusieurs sources de données locales.
* Vous pouvez connecter plusieurs passerelles sur différents ordinateurs à la même source de données locale.
* Vous ne configurez une passerelle que pour un seul espace de travail à la fois. Pour le moment, les passerelles ne peuvent pas être partagées entre plusieurs espaces de travail.
* Vous pouvez configurer plusieurs passerelles pour un espace de travail unique. Par exemple, vous pouvez choisir d’utiliser une passerelle connectée à vos sources de données de test lors du développement et une passerelle de production lorsque vous êtes prêt pour l’opérationnalisation.
* La passerelle n’a pas besoin d’être sur le même ordinateur que la source de données. Toutefois, le fait d’avoir une passerelle plus proche de la source de données réduit le temps de connexion de la passerelle à la source de données. Nous vous recommandons d’installer la passerelle sur un ordinateur différent de celui qui héberge la source de données locale, afin que la passerelle et la source de données ne soient pas en concurrence pour l’attribution de ressources.
* Si une passerelle est déjà installée sur votre ordinateur desservant des scénarios Power BI ou Azure Data Factory, installez une passerelle distincte pour Azure Machine Learning sur un autre ordinateur.

  > [!NOTE]
  > Vous ne pouvez pas exécuter la passerelle de gestion des données et la passerelle Power BI sur le même ordinateur.
  >
  >
* Vous devez utiliser la passerelle de gestion des données pour Azure Machine Learning, même si vous utilisez Azure ExpressRoute pour d’autres données. Traitez votre source de données comme une source de données locale (derrière un pare-feu), même quand vous utilisez ExpressRoute. Utilisez la passerelle de gestion des données pour établir la connectivité entre Machine Learning et la source de données.

Vous trouverez des informations détaillées sur les prérequis pour l’installation, des étapes d’installation et des conseils de dépannage dans l’article [Passerelle de gestion des données](../../data-factory/v1/data-factory-data-management-gateway.md).

## <a name="span-idusing-the-data-gateway-step-by-step-walk-classanchorspan-idtoc450838866-classanchorspanspaningress-data-from-your-on-premises-sql-server-database-into-azure-machine-learning"></a><span id="using-the-data-gateway-step-by-step-walk" class="anchor"><span id="_Toc450838866" class="anchor"></span></span>Intégrer des données de votre base de données SQL Server locale dans Azure Machine Learning
Dans cette procédure pas à pas, vous allez configurer une passerelle de gestion des données dans un espace de travail Azure Machine Learning, la configurer, puis lire les données à partir d’une base de données SQL Server locale.

> [!TIP]
> Avant de commencer, désactivez le bloqueur de fenêtres publicitaires de votre navigateur pour `studio.azureml.net`. Si vous utilisez le navigateur Google Chrome, téléchargez et installez l’un des modules disponibles sur le WebStore de Google Chrome [Extension de l’application Click Once](https://chrome.google.com/webstore/search/clickonce?_category=extensions).
>
>

### <a name="step-1-create-a-gateway"></a>Étape 1 : Créer une passerelle
La première étape consiste à créer et à configurer la passerelle pour accéder à votre base de données SQL locale.

1. Connectez-vous à [Azure Machine Learning Studio](https://studio.azureml.net/Home/) et sélectionnez l’espace de travail dans lequel vous souhaitez travailler.
2. Cliquez sur le panneau **PARAMÈTRES** sur la gauche, puis cliquez sur l’onglet **PASSERELLES DE DONNÉES** en haut.
3. Cliquez sur **NOUVELLE PASSERELLE DE DONNÉES** en bas de l’écran.

    ![Nouvelle passerelle de données](./media/use-data-from-an-on-premises-sql-server/new-data-gateway-button.png)
4. Dans la boîte de dialogue **Nouvelle passerelle de données**, entrez le **Nom de la passerelle** et ajoutez éventuellement une **Description**. Cliquez sur la flèche située dans l’angle inférieur droit pour accéder à l’étape suivante de la configuration.

    ![Entrez la description et le nom de la passerelle](./media/use-data-from-an-on-premises-sql-server/new-data-gateway-dialog-enter-name.png)
5. Dans la boîte de dialogue Télécharger et inscrire une passerelle de données, copiez la CLÉ D’INSCRIPTION DE LA PASSERELLE dans le presse-papiers.

    ![Téléchargez et enregistrez la passerelle de données](./media/use-data-from-an-on-premises-sql-server/download-and-register-data-gateway.png)
6. <span id="note-1" class="anchor"></span>Si vous n’avez pas encore téléchargé et installé la passerelle de gestion des données de Microsoft, cliquez sur **Télécharger la passerelle de gestion des données**. Vous accéderez au Centre de téléchargement Microsoft, où vous pourrez sélectionner la version de la passerelle dont vous avez besoin, la télécharger et l’installer. Vous trouverez des informations détaillées sur les conditions préalables à l’installation, des étapes d’installation et des conseils de dépannage dans les sections du début de l’article [Déplacer des données entre des sources locales et le cloud à l’aide de la passerelle de gestion des données](../../data-factory/v1/data-factory-move-data-between-onprem-and-cloud.md).
7. Une fois la passerelle installée, le Gestionnaire de configuration de la passerelle de gestion des données s’ouvre et la boîte de dialogue **Inscrire la passerelle** s’affiche. Collez la **Clé d’inscription de la passerelle** que vous avez copiée dans le presse-papiers et cliquez sur **Inscrire**.
8. Si vous avez déjà installé une passerelle, exécutez le Gestionnaire de configuration de la passerelle de gestion des données. Cliquez sur **Modifier la clé**, collez la **Clé d’inscription de la passerelle** que vous avez copiée dans le Presse-papiers à l’étape précédente, puis cliquez sur **OK**.
9. Une fois l’installation terminée, la boîte de dialogue **Inscrire la passerelle** du Gestionnaire de configuration de la passerelle de gestion des données de Microsoft s’affiche. Collez la CLÉ D’INSCRIPTION DE LA PASSERELLE que vous avez copiée dans le Presse-papiers lors d’une étape précédente et cliquez sur **Inscrire**.

    ![Inscrivez la passerelle](./media/use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-register-gateway.png)
10. La configuration de la passerelle est terminée lorsque les valeurs suivantes sont définies sur l’onglet **Accueil** dans le Gestionnaire de configuration de la passerelle de gestion des données de Microsoft :

    * **Nom de la passerelle** et **Nom de l’instance** sont définis sur le nom de la passerelle.
    * **Inscription** est défini sur **Inscrit**.
    * **État** est défini sur **Démarré**.
    * La barre d’état située au bas de l’écran affiche le message **Connecté au service cloud de la passerelle de gestion des données** accompagné d’une coche verte.

      ![Gestionnaire de passerelle de gestion de données](./media/use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-registered.png)

      Azure Machine Learning Studio se met également à jour lorsque l’inscription réussit.

    ![Inscription de la passerelle réussie](./media/use-data-from-an-on-premises-sql-server/gateway-registered.png)
11. Dans la boîte de dialogue **Télécharger et inscrire la passerelle de données** , cliquez sur la coche pour terminer l’installation. La page **Paramètres** affiche l’état « En ligne » pour la passerelle. Dans le volet de droite, vous trouverez l’état et d’autres informations utiles.

    ![Paramètres de la passerelle](./media/use-data-from-an-on-premises-sql-server/gateway-status.png)
12. Dans le Gestionnaire de configuration de la passerelle de gestion des données de Microsoft, basculez vers l’onglet **Certificat** . Le certificat spécifié dans cet onglet sert à chiffrer/déchiffrer les informations d’identification pour le magasin de données local que vous spécifiez dans le portail. Il s’agit du certificat par défaut. Microsoft recommande de le modifier pour spécifier votre propre certificat, que vous sauvegardez dans votre système de gestion des certificats. Cliquez sur **Modifier** pour utiliser votre propre certificat à la place.

    ![Changez le certificat de la passerelle](./media/use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-certificate.png)
13. (Facultatif) Si vous souhaitez activer la journalisation détaillée pour résoudre les problèmes de passerelle, dans le Gestionnaire de configuration de la passerelle de gestion des données de Microsoft, basculez sur l’onglet **Diagnostics** et cochez l’option **Activer la journalisation détaillée pour résoudre des problèmes**. Vous trouverez les informations de journalisation dans l’Observateur d’événements Windows sous le nœud **Journaux des applications et des services** -&gt; **Passerelle de gestion des données**. Vous pouvez également utiliser l’onglet **Diagnostics** pour tester la connexion à une source de données locale à l’aide de la passerelle.

    ![Activez la journalisation commentée](./media/use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-verbose-logging.png)

Le processus de configuration de la passerelle dans Azure Machine Learning est terminé.
Vous êtes maintenant prêt à utiliser vos données locales.

Vous pouvez créer et configurer plusieurs passerelles dans Studio pour chaque espace de travail. Par exemple, vous pouvez avoir une passerelle que vous souhaitez connecter à vos sources de données de test pendant le développement et une passerelle distincte pour vos sources de données en production. Azure Machine Learning vous donne la possibilité de configurer plusieurs passerelles en fonction de votre environnement d’entreprise. Actuellement, vous ne pouvez pas partager une passerelle entre différents espaces de travail et une seule passerelle peut être installée sur un même ordinateur. Pour plus d’informations, consultez [Déplacement de données entre des sources locales et le cloud à l’aide de la passerelle de gestion des données](../../data-factory/v1/data-factory-move-data-between-onprem-and-cloud.md).

### <a name="step-2-use-the-gateway-to-read-data-from-an-on-premises-data-source"></a>Étape 2 : Utiliser la passerelle pour lire des données à partir d’une source de données locale
Après avoir configuré la passerelle, vous pouvez ajouter un module **Importer des données** à une expérience qui prend en entrée les données de la base de données SQL Server locale.

1. Dans Machine Learning Studio, sélectionnez l’onglet **EXPÉRIENCES** cliquez sur **+NOUVELLE** dans le coin inférieur gauche, puis sélectionnez **Expérience vide** (ou sélectionnez l’un des exemples d’expérimentations disponibles).
2. Recherchez et faites glisser le module **Importer des données** jusqu’à la zone de dessin de l’expérience.
3. Cliquez sur **Enregistrer sous** sous le canevas. Entrez « Didacticiel SQL Server local Azure Machine Learning » comme nom de l’expérience, sélectionnez l’espace de travail, puis cochez la case **OK** .

   ![Enregistrez l’expérience sous un nouveau nom](./media/use-data-from-an-on-premises-sql-server/experiment-save-as.png)
4. Cliquez sur le module **Importer des données** pour le sélectionner puis, dans le volet **Propriétés** à droite de la zone de dessin, sélectionnez « Base de données SQL locale » dans la liste déroulante **Source de données**.
5. Sélectionnez la **Passerelle de données** que vous avez installée et inscrite. Vous pouvez configurer une autre passerelle en sélectionnant « (ajouter une nouvelle passerelle de données...) ».

   ![Sélectionnez une passerelle de données pour le module d’importation de données](./media/use-data-from-an-on-premises-sql-server/import-data-select-on-premises-data-source.png)
6. Entrez le **Nom du serveur de base de données** et le **Nom de la base de données** SQL, ainsi que la **Requête de base de données** SQL que vous souhaitez exécuter.
7. Cliquez sur **Entrer des valeurs** sous **Nom d’utilisateur et mot de passe** et entrez vos informations d’identification de base de données. Vous pouvez utiliser l’authentification intégrée Windows ou l’authentification SQL Server en fonction de la configuration de votre serveur local SQL Server.

   ![Entrez les informations d’identification de la base de données](./media/use-data-from-an-on-premises-sql-server/database-credentials.png)

   Le message « valeurs requises » devient « valeurs définies » avec une coche verte. Il vous suffit d’entrer les informations d’identification une seule fois, sauf si les informations de base de données ou de mot de passe changent. Azure Machine Learning utilise le certificat que vous avez fourni lors de l’installation de la passerelle pour chiffrer les informations d’identification dans le cloud. Azure ne stocke jamais d’informations d’identification locales sans chiffrement.

   ![Importez les propriétés du module de données](./media/use-data-from-an-on-premises-sql-server/import-data-properties-entered.png)
8. Cliquez sur **EXÉCUTER** pour lancer l’expérience.

Une fois l’expérimentation terminée, vous pouvez visualiser les données que vous avez importées à partir de la base de données en cliquant sur le port de sortie du module **Importer des données** et en sélectionnant **Visualiser**.

Une fois que vous avez terminé le développement de votre expérience, vous pouvez déployer et opérationnaliser votre modèle. Grâce au service d’exécution de lots, les données de la base de données SQL Server locale configurées dans le module **Importer des données** seront lues et utilisées pour l’évaluation. Vous pouvez utiliser le service de réponse aux demandes pour l’évaluation des données locales, mais Microsoft recommande d’utiliser plutôt le [complément Excel](excel-add-in-for-web-services.md) . Actuellement, l’écriture dans une base de données SQL Server locale avec **Exporter des données** n’est pas prise en charge dans vos expériences ou dans les services web publiés.
