---
title: aaaCreate un espace de travail Machine Learning | Documents Microsoft
description: Comment toocreate un espace de travail pour Azure Machine Learning Studio
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: aa96b784-ac6c-44bc-a28a-85d49fbe90a2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye;bradsev;ahgyger
ms.openlocfilehash: 178293af222365993fade666124f34269d892325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-an-azure-machine-learning-workspace"></a>Créer et partager un espace de travail Azure Machine Learning
Ce menu lie tootopics qui décrivent comment tooset des hello différents environnements de science des données utilisé par hello Cortana Analytique processus (CAP).

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

toouse Azure Machine Learning Studio, vous devez toohave un espace de travail Machine Learning. Cet espace de travail contienne des outils de hello vous devez toocreate, gérer et publier des expériences.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="toocreate-a-workspace"></a>toocreate un espace de travail
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/)

    > [!NOTE]
    > toosign dans et créer un espace de travail, vous devez toobe administrateur d’abonnement Azure. 
    >
    > 

2. Cliquez sur **+Nouveau**.

3. Sélectionnez **Intelligence + analyse**, puis cliquez sur **Espace de travail Machine Learning** et sur **Créer**.

4. Entrez vos informations d’espace de travail.

    - Hello *nom de l’espace de travail* peuvent être des caractères too260, se termine ne pas par un espace. nom de Hello ne peut pas contenir ces caractères :`< > * % & : \ ? + /`
    - Hello *plan de service web* vous choisissez (ou créer), ainsi que de hello associé *tarification* vous sélectionnez, est utilisé si vous déployez des services web à partir de cet espace de travail.

    ![Créer un espace de travail](media/machine-learning-create-workspace/create-new-workspace.png)

5. Cliquez sur **Créer**

Une fois que l’espace de travail hello est déployé, vous pouvez l’ouvrir dans Machine Learning Studio.

1. Parcourir tooMachine Learning Studio à [https://studio.azureml.net/](https://studio.azureml.net/).

2. Sélectionnez votre espace de travail dans l’angle supérieure droite de hello.

    ![Sélectionner un espace de travail](media/machine-learning-create-workspace/open-workspace.png)

3. Cliquez sur **my experiments (mes expérimentations)**.

    ![Ouvrir des expérimentations](media/machine-learning-create-workspace/my-experiments.png)

Pour plus d’informations sur la gestion de votre espace de travail, consultez [Gestion d’un espace de travail Azure Machine Learning](machine-learning-manage-workspace.md).
Si vous rencontrez un problème de création de votre espace de travail, consultez [guide de dépannage : créer et connecter l’espace de travail Machine Learning tooa](machine-learning-troubleshooting-creating-ml-workspace.md).


## <a name="sharing-an-azure-machine-learning-workspace"></a>Partage d’un espace de travail Azure Machine Learning
Une fois qu’un espace de travail Machine Learning est créé, vous pouvez inviter les utilisateurs tooyour espace de travail tooshare accès tooyour espace de travail et tous les ses expériences, jeux de données, ordinateurs portables, etc.. Vous pouvez ajouter des utilisateurs dans l’un des deux rôles :

* **Utilisateur** -un utilisateur de l’espace de travail peut créer, ouvrir, modifier et supprimer des expériences, jeux de données, etc. dans l’espace de travail hello.
* **Propriétaire** - invite un propriétaire et supprimer des utilisateurs dans hello espace de travail, ajout toowhat un utilisateur peuvent faire.

> [!NOTE]
> compte d’administrateur Hello qui crée l’espace de travail hello est automatiquement ajouté toohello espace de travail en tant que propriétaire de l’espace de travail. Toutefois, autres administrateurs ou des utilisateurs dans la mesure où abonnement ne sont pas automatiquement accordé l’accès toohello espace de travail : vous devez tooinvite les explicitement.
> 
> 

### <a name="tooshare-a-workspace"></a>tooshare un espace de travail

1. Se connecter tooMachine Learning Studio à [https://studio.azureml.net/Home](https://studio.azureml.net/Home)

2. Dans le volet gauche de hello, cliquez sur **paramètres**

3. Cliquez sur hello **utilisateurs** onglet

4. Cliquez sur **inviter des utilisateurs plus** bas hello de page de hello

    ![Paramètres Studio](media/machine-learning-create-workspace/settings.png)

5. Entrez une ou plusieurs adresses e-mail. les utilisateurs de Hello besoin d’un compte Microsoft valide ou un compte professionnel (à partir d’Azure Active Directory).

6. Sélectionnez si vous souhaitez que les utilisateurs de hello tooadd en tant que propriétaire ou utilisateur.

7. Cliquez sur hello **OK** coche.

Chaque utilisateur que vous ajoutez recevra un e-mail contenant des instructions sur le mode de partage de l’espace de travail de toosign dans toohello.

> [!NOTE]
> Pour toodeploy en mesure de toobe les utilisateurs ou gérer des services web dans cet espace de travail, ils doivent être un contributeur ou un administrateur Bonjour abonnement Azure. 



