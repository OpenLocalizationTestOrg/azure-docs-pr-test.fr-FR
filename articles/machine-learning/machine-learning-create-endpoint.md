---
title: "points de terminaison du service aaaCreating Web dans l’apprentissage | Documents Microsoft"
description: "Création de points de terminaison de service web dans Azure Machine Learning"
services: machine-learning
documentationcenter: 
author: hiteshmadan
manager: padou
editor: cgronlun
ms.assetid: 4657fc1b-5228-4950-a29e-bc709259f728
ms.service: machine-learning
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 10/04/2016
ms.author: himad
ms.openlocfilehash: 10a2bc586c6fe35e28d8bf0293854c578827c453
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-endpoints"></a>Création de points de terminaison
> [!NOTE]
>  Cette rubrique décrit les techniques des tooa applicable **classique** service Machine Learning Web.
> 
> 

Lorsque vous créez des services Web qui vendent des clients de tooyour vers l’avant, vous devez tooprovide modèles formés tooeach client expérience toohello toujours lié à partir de quels hello Web service a été créé. En outre, les mises à jour toohello expérience doit-elle être appliquent de manière sélective tooan le point de terminaison sans remplacer les personnalisations hello.

tooaccomplish, Azure Machine Learning vous permet de toocreate plusieurs points de terminaison pour un service Web déployé. Chaque point de terminaison de service Web de hello est indépendamment adressé limitée et géré. Chaque point de terminaison est une clé unique d’URL et d’autorisation que vous pouvez distribuer tooyour clients.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="adding-endpoints-tooa-web-service"></a>Ajout de service Web de tooa points de terminaison
Il existe trois façons tooadd un tooa de point de terminaison service Web.

* Par programmation
* Via le portail de Services Web de Azure Machine Learning hello
* Bien que hello portail Azure classic

Une fois que le point de terminaison hello est créé, vous pouvez consommer via les API synchrones, lot API et feuilles de calcul excel. En outre tooadding les points de terminaison via cette interface utilisateur, vous pouvez également utiliser hello API de gestion de point de terminaison tooprogrammatically ajouter des points de terminaison.

> [!NOTE]
> Si vous avez ajouté des points de terminaison supplémentaires toohello service Web, vous ne pouvez pas supprimer le point de terminaison par défaut hello.
> 
> 

## <a name="adding-an-endpoint-programmatically"></a>Ajout d’un point de terminaison par programme
Vous pouvez ajouter un point de terminaison tooyour Web service par programme hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) exemple de code.

## <a name="adding-an-endpoint-using-hello-azure-machine-learning-web-services-portal"></a>Ajout d’un point de terminaison à l’aide du portail de Services Web de Azure Machine Learning hello
1. Dans Machine Learning Studio, sur la colonne du volet de navigation gauche hello, cliquez sur les Services Web.
2. Au bas de hello du tableau de bord de service Web hello, cliquez sur **gérer les points de terminaison**. portail de Services Web de Azure Machine Learning Hello ouvre la page de points de terminaison de toohello pourquoi le service Web.
3. Cliquez sur **Nouveau**.
4. Tapez un nom et une description pour le nouveau point de terminaison hello. Les noms de point de terminaison doivent compter au maximum 24 caractères, et doivent être composés de lettres minuscules ou de chiffres. Sélectionnez le niveau de journalisation hello et indique si les exemples de données sont activées. Pour plus d’informations sur la journalisation, voir [Activation de la journalisation pour les services web Machine Learning](machine-learning-web-services-logging.md).

## <a name="adding-an-endpoint-using-hello-azure-classic-portal"></a>Ajout d’un point de terminaison à l’aide de hello portail Azure classic
1. Connectez-vous à toohello [portail Azure classic](http://manage.windowsazure.com), cliquez sur **Machine Learning** dans la colonne de gauche hello. Cliquez sur espace de travail hello qui contient le service Web de hello qui vous intéressent.
   
    ![Accédez tooworkspace](./media/machine-learning-create-endpoint/figure-1.png)
2. Cliquez sur **Services web**.
   
    ![Accédez tooWeb services](./media/machine-learning-create-endpoint/figure-2.png)
3. Cliquez sur le service Web de hello vous intéresse dans la liste de hello toosee de points de terminaison disponibles.
   
    ![Accédez tooendpoint](./media/machine-learning-create-endpoint/figure-3.png)
4. Au bas de hello de page de hello, cliquez sur **ajouter le point de terminaison**. Tapez un nom et une description, vérifiez qu’aucun autre point de terminaison avec le même nom dans ce service Web de hello. Laissez le niveau de limitation de bande passante de hello avec sa valeur par défaut, sauf si vous avez des spécifications spéciales. toolearn en savoir plus sur la limitation, consultez [API points de terminaison de mise à l’échelle](machine-learning-scaling-webservice.md).
   
    ![Création d’un point de terminaison](./media/machine-learning-create-endpoint/figure-4.png)

## <a name="next-steps"></a>Étapes suivantes
[Comment tooconsume un service Web de Azure Machine Learning](machine-learning-consume-web-services.md).

