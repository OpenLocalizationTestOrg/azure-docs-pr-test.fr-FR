---
title: "complément aaaExcel pour les services Web d’apprentissage Machine | Documents Microsoft"
description: "Comment toouse Azure Machine Learning Web services directement dans Excel sans écrire de code."
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 9618079d-502f-4974-a3e2-8f924042a23f
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/14/2017
ms.author: tedway;garye
ms.openlocfilehash: c52f40d33c9907f284e4750afe47181dc3365fe5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="excel-add-in-for-azure-machine-learning-web-services"></a>Complément Excel de services web Azure Machine Learning
Excel rend toocall facilement des services web directement sans hello besoin toowrite n’importe quel code.

## <a name="steps-toouse-an-existing-web-service-in-hello-workbook"></a>Étapes tooUse un service web existant hello classeur

1. Ouvrez hello [exemple de fichier Excel](http://aka.ms/amlexcel-sample-2), qui contient du complément Excel hello et données concernant les passagers sur hello TITANE.
2. Choisissez le service web de hello en cliquant dessus-« Titanic survivant PRÉDICTEUR (exemple de complément Excel) [Score] » dans cet exemple.
   
    ![Sélectionner un service web][01]
3. Vous accéderez toohello **Predict** section.  Ce classeur contient déjà des exemples de données mais, pour un classeur vide, vous pouvez également sélectionner une cellule dans Excel et cliquer sur **Utiliser les exemples de données**.
4. Sélectionnez les données hello avec les en-têtes, puis cliquez sur icône des tranches de données d’entrée hello.  Vérifiez que hello « mes données comportent des en-têtes » est activée.
5. Sous **sortie**, entrez le nombre de cellules hello hello toobe de sortie, par exemple « H1 » ici.
6. Cliquez sur **Prédire**.
   
    ![Section Prédire][02]

Déployez un service web ou utilisez un service web existant. Pour plus d’informations sur le déploiement d’un service web, consultez [procédure pas à pas étape 5 : déployer le service d’Azure Machine Learning Web hello](machine-learning-walkthrough-5-publish-web-service.md).

Obtenir la clé d’API hello pour votre service web. L’emplacement à partir duquel exécutez cette action diffère selon que vous avez publié un service web Machine Learning classique ou un nouveau service web Machine Learning.

**Utiliser un service web classique** 

1. Dans Machine Learning Studio, cliquez sur hello **SERVICES WEB** section dans le volet gauche de hello, puis sélectionnez le service web de hello.
   
    ![Studio - Sélectionner un service web][04]
2. Copiez la clé d’API hello pour le service web de hello.
   
    ![Studio clé API][05]
3. Sur hello **tableau de bord** pour le service web de hello, cliquez sur hello **demande/réponse** lien.
4. Recherchez hello **URI de requête** section.  Copiez et enregistrez l’URL de hello.

> [!NOTE]
> Il est désormais possible toosign dans hello [Azure Machine Learning Web Services](https://services.azureml.net) clé de hello API tooobtain portail pour un service web d’apprentissage classique.
> 
> 

**Utiliser un nouveau service web**

1. Bonjour [Azure Machine Learning Web Services](https://services.azureml.net) portail, cliquez sur **Services Web**, puis sélectionnez votre service web. 
2. Cliquez sur **Consommer**.
3. Recherchez hello **les informations de base de la consommation** section. Copiez et enregistrez hello **clé primaire** et hello **demande-réponse** URL.

## <a name="steps-tooadd-a-new-web-service"></a>Étapes tooAdd un nouveau service web

1. Déployez un service web ou utilisez un service web existant. Pour plus d’informations sur le déploiement d’un service web, consultez [procédure pas à pas étape 5 : déployer le service d’Azure Machine Learning Web hello](machine-learning-walkthrough-5-publish-web-service.md).
2. Cliquez sur **Consommer**.
3. Recherchez hello **les informations de base de la consommation** section. Copiez et enregistrez hello **clé primaire** et hello **demande-réponse** URL.
4. Dans Excel, accédez à toohello **Services Web** section (si vous êtes dans hello **Predict** , cliquez sur la liste de toohello toogo hello flèche précédent de services web).
   
    ![Atteindre la sélection du service tooWeb][03]
5. Cliquez sur **Ajouter un service web**.
6. Collez les URL hello hello Excel intitulé de la zone de texte du complément **URL**.
7. Clé d’API/primaire de hello coller dans la zone de texte hello **clé API**.
8. Cliquez sur **Add**.
   
    ![URL et clé API pour un service web classique.][06]
9. service web de hello toouse, suivez hello précédant directions, « Étapes tooUse un Service de serveur web existant ».

## <a name="sharing-your-workbook"></a>Partage de votre classeur
Si vous enregistrez votre classeur, puis clé d’API/primaire hello pour les services web hello que vous avez ajouté est également enregistré. Cela signifie que vous devez uniquement partager les classeur hello avec des personnes de que confiance.

Poser des questions dans hello suivant la section commentaires ou sur notre [forum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).

[01]: ./media/machine-learning-excel-add-in-for-web-services/image1.png
[02]: ./media/machine-learning-excel-add-in-for-web-services/image2.png
[03]: ./media/machine-learning-excel-add-in-for-web-services/image3.png
[04]: ./media/machine-learning-excel-add-in-for-web-services/image4.png
[05]: ./media/machine-learning-excel-add-in-for-web-services/image5.png
[06]: ./media/machine-learning-excel-add-in-for-web-services/image6.png
