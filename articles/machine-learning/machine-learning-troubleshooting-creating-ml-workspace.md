---
title: "Résoudre les problèmes : Création et la connexion d’espace de travail Machine Learning tooa | Documents Microsoft"
description: "Solutions aux problèmes courants dans la création et l’espace de travail Azure Machine Learning tooan de connexion"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 1a8aec4b-35f9-44e8-9570-2575b8979ab1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 965a0025e85ba4e22c2b037edfa923e7f7599069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-create-and-connect-tooan-machine-learning-workspace"></a>Guide de dépannage : créer et connecter l’espace de travail Machine Learning tooan
Ce guide propose des solutions pour quelques-uns des défis qui se posent souvent quand vous configurez des espaces de travail Azure Machine Learning.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="workspace-owner"></a>Propriétaire de l'espace de travail
tooopen un espace de travail dans Machine Learning Studio, vous devez être connecté toohello Account Microsoft, vous avez utilisé l’espace de travail de toocreate hello, ou si vous devez tooreceive une invitation à partir de l’espace de travail hello propriétaire toojoin hello. À partir de hello portail Azure, vous pouvez gérer hello espace de travail, qui inclut l’accès de tooconfigure possibilité hello.

Pour plus d'informations sur la gestion d'un espace de travail, consultez [Gestion d'un espace de travail Azure Machine Learning].

[Gestion d'un espace de travail Azure Machine Learning]: machine-learning-manage-workspace.md

## <a name="allowed-regions"></a>Régions autorisées
Machine Learning est actuellement disponible dans un nombre limité de régions. Si votre abonnement n’inclut pas un de ces régions, vous pouvez voir le message d’erreur hello, « Vous n’avez aucun abonnement Bonjour autorisé régions. »

toorequest une région être ajouté tooyour abonnement, créer une nouvelle demande de support Microsoft à partir de hello portail Azure, choisissez **facturation** en tant que type de problème hello et suivez hello invite toosubmit votre demande.

## <a name="storage-account"></a>Compte de stockage
Hello service Machine Learning a besoin de données de toostore d’un compte de stockage. Vous pouvez utiliser un compte de stockage existant, ou vous pouvez créer un compte de stockage lorsque vous créez hello apprentissage espace de travail (si vous avez un compte de stockage à quota toocreate).

Après la création de l’espace de travail de Machine Learning nouvelle hello, vous pouvez signer dans tooMachine Learning Studio à l’aide du compte Microsoft de hello que vous avez utilisé l’espace de travail toocreate hello. Si vous rencontrez le message d’erreur hello, « Espace de travail introuvable » (toohello similaire après la capture d’écran), utilisez hello suivant les étapes toodelete les cookies de votre navigateur.

![Workspace not found][screen3]

**cookies du navigateur toodelete**

1. Si vous utilisez Internet Explorer, cliquez sur hello **outils** situé dans le coin supérieur droit de hello et sélectionnez **options Internet**.  

![Options Internet][screen4]

2. Sous hello **général** , cliquez sur **supprimer...**

![General tab][screen5]

3. Bonjour **supprimer l’historique de navigation** boîte de dialogue zone, assurez-vous que **les Cookies et les données du site Web** est sélectionné, puis cliquez sur **supprimer**.

![Delete cookies][screen6]

Une fois que les cookies de hello sont supprimés, redémarrez le navigateur de hello et passez toohello [Microsoft Azure Machine Learning](https://studio.azureml.net) page. Lorsque vous êtes invité à saisir un nom d’utilisateur et un mot de passe, entrez hello même compte Microsoft que vous avez utilisé l’espace de travail toocreate hello.

## <a name="comments"></a>Commentaires

Notre objectif est toomake hello expérience d’apprentissage plus transparente possible. Envoyez des commentaires et des problèmes à hello [forum d’Azure Machine Learning](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) toohelp nous mieux vous servir.

[screen1]:media/machine-learning-troubleshooting-creating-ml-workspace/screen1.png
[screen2]:media/machine-learning-troubleshooting-creating-ml-workspace/screen2.png
[screen3]:media/machine-learning-troubleshooting-creating-ml-workspace/screen3.png
[screen4]:media/machine-learning-troubleshooting-creating-ml-workspace/screen4.png
[screen5]:media/machine-learning-troubleshooting-creating-ml-workspace/screen5.png
[screen6]:media/machine-learning-troubleshooting-creating-ml-workspace/screen6.png
