---
title: "flux de travail aaaCreate à partir de modèles - Azure Logic Apps | Documents Microsoft"
description: "Prise en main - créer rapidement des flux de travail à l’aide de l’application Azure logique modèles tooconnect applications et intégrer des données."
author: kevinlam1
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 3656acfb-eefd-4e75-b5d2-73da56c424c9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: LADocs; klam
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0127523662a12076772b52968f1e2f9cbad72a1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-workflow-using-a-pre-built-template-or-pattern-tooget-started-quickly"></a>Configurer un flux de travail à l’aide d’un modèle prédéfini ou un tooget modèle démarré rapidement

## <a name="what-are-logic-app-templates"></a>Qu’est-ce qu’un modèle d’application logique ?
Un modèle d’application logique est une application logique préconstruit que vous pouvez utiliser tooquickly prise en main de la création de votre propre flux de travail. 

Ces modèles est un bon moyen toodiscover divers modèles qui peuvent être générées à l’aide d’applications de la logique. Vous pouvez utiliser ces modèles comme-est ou modifiez-les toofit votre scénario.

## <a name="overview-of-available-templates"></a>Vue d’ensemble des modèles disponibles
Il existe de nombreux modèles disponibles actuellement publiés dans la plateforme d’application hello logique. Certaines catégories d’exemples, ainsi que type hello de connecteurs utilisés, est répertoriée ci-dessous.

### <a name="enterprise-cloud-templates"></a>Modèles de cloud d’entreprise
Il s’agit de modèles qui s’intègrent à Dynamics CRM, Salesforce, Box, Azure Blob et d’autres connecteurs pour les besoins de votre cloud d’entreprise. L’organisation de vos prospects et l’enregistrement des données de vos fichiers d’entreprise figurent parmi les possibilités offertes par ces modèles.

### <a name="enterprise-integration-pack-templates"></a>Modèles de pack d’intégration d’entreprise
Configurations de VETER (valider, extraire, transformer, enrichir, Router) reçoit un X12 EDI via AS2 de document et transformant tooXML, ainsi que le message X12 et AS2 gestion des pipelines.

### <a name="protocol-pattern-templates"></a>Modèles de modèles de protocole
Ces modèles se composent d’applications logiques contenant des modèles de protocole comme une demande-réponse via HTTP, ainsi que des intégrations sur FTP et SFTP. Utilisez-les tels qu’ils existent, ou comme base pour la création de modèles de protocole plus complexes.  

### <a name="personal-productivity-templates"></a>Modèles de productivité personnelle
Modèles toohelp améliorer la productivité personnelles incluent des modèles de définir des rappels quotidiennes, activer des éléments de travail importantes dans les listes de tâches et automatisent des tâches de longue durée vers le bas l’étape d’approbation tooa utilisateur unique.

### <a name="consumer-cloud-templates"></a>Modèles Cloud clients
Il s’agit de modèles simples qui s’intègrent aux services des médias sociaux, tels que Twitter, Slak et aux messageries, et capables d’en renforcer les initiatives marketing. Parmi ceux-ci figurent également les modèles, tels que la copie dans le cloud qui permettent d’augmenter la productivité en passant moins de temps sur les tâches traditionnellement répétitives. 

## <a name="how-toocreate-a-logic-app-using-a-template"></a>Comment toocreate une application logique à l’aide d’un modèle
tooget démarré à l’aide d’un modèle d’application logique, allez dans le Concepteur d’application hello logique. Si vous saisissez le concepteur hello en ouvrant une application existante de la logique, hello logique application charge automatiquement dans votre vue du concepteur. Toutefois, si vous créez une nouvelle application logique, vous consultez écran hello ci-dessous.  
 ![](../../includes/media/app-service-logic-templates/template7.png)  

À partir de cet écran, vous pouvez choisir toostart avec une application logique vide ou un modèle prédéfini. Si vous sélectionnez un des modèles de hello, vous sont fournies avec des informations supplémentaires. Dans cet exemple, nous utilisons hello *lorsqu’un nouveau fichier est créé dans Dropbox, copiez-le tooOneDrive* modèle.  
 ![](../../includes/media/app-service-logic-templates/template2.png)  

Si vous choisissez le modèle de hello toouse, sélectionnez simplement hello *utiliser ce modèle* bouton. Vous serez invité à indiquer toosign de comptes tooyour basé sur le modèle de hello connecteurs utilise. Si vous avez déjà établi une connexion avec ces connecteurs, vous pouvez également choisir de continuer comme indiqué ci-dessous.  
 ![](../../includes/media/app-service-logic-templates/template3.png)  

Après l’établissement de connexions de hello et en sélectionnant *continuer*, application de hello logique s’ouvre en mode concepteur.  
 ![](../../includes/media/app-service-logic-templates/template4.png)  

Dans l’exemple hello ci-dessus, comme dans les cas de hello avec de nombreux modèles, certains champs de propriété obligatoire hello peuvent être rempli dans les connecteurs hello ; Toutefois, certaines peuvent nécessiter toujours une valeur avant de pouvoir tooproperly déployer l’application logique de hello. Si vous essayez toodeploy sans entrer de certains des champs manquants de hello, vous serez averti avec un message d’erreur.

Si vous souhaitez la visionneuse de modèle tooreturn toohello, sélectionnez hello *modèles* bouton dans la barre de navigation supérieure hello. En basculant la visionneuse de modèle toohello précédent, vous perdez toute progression non enregistrée. Tooswitching préalable dans la visionneuse de modèle, vous verrez un message d’avertissement vous informe de cette.  
 ![](../../includes/media/app-service-logic-templates/template5.png)  

## <a name="how-toodeploy-a-logic-app-created-from-a-template"></a>Comment toodeploy une application logique créé à partir d’un modèle
Une fois que vous avez chargé votre modèle et apporté des modifications de votre choisies, sélectionnez hello bouton Enregistrer dans le coin supérieur gauche de hello. Cela enregistre et publie votre application logique.  
 ![](../../includes/media/app-service-logic-templates/template6.png)  

Si vous souhaitez plus d’informations sur comment tooadd étapes plus dans un modèle d’application logique existant, ou apporter des modifications en général, en savoir plus sur [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).

