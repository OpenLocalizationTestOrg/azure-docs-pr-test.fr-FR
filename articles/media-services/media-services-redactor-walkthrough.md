---
title: "faces aaaRedact avec Azure Media Analytique procédure pas à pas | Documents Microsoft"
description: "Cette rubrique présente des instructions étape par étape sur la façon de toorun un flux de travail de rédaction complète à l’aide d’Azure Media Services Explorer (AMSE) et Azure Media Redactor visualiseur (outil open source)."
services: media-services
documentationcenter: 
author: Lichard
manager: cfowler
editor: 
ms.assetid: d6fa21b8-d80a-41b7-80c1-ff1761bc68f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/03/2017
ms.author: rli; juliako;
ms.openlocfilehash: ab28f4052b73fdb74fcd5766235eab35402a0c9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics-walkthrough"></a>Procédure d’édition des visages avec Azure Media Analytics

## <a name="overview"></a>Vue d'ensemble

**Azure Media Redactor** est un [Azure Media Analytique](media-services-analytics-overview.md) processeur multimédia (MP) qui offre la rédaction de face évolutives dans le cloud de hello. Rédaction de face permet de vous toomodify votre vidéo dans faces de tooblur d’ordre d’individus sélectionnés. Vous pouvez choisir de service de rédaction face toouse hello dans les scénarios de sécurité et de médias public. Quelques minutes de film qui contient plusieurs polices peuvent prendre des heures tooredact manuellement, mais avec cette face hello de service des processus de rédaction nécessite quelques étapes simples. Pour plus d’informations, consultez [ce blog](https://azure.microsoft.com/blog/azure-media-redactor/).

Pour plus d’informations sur les **Azure Media Redactor**, consultez hello [vue d’ensemble de la rédaction Face](media-services-face-redaction.md) rubrique.

Cette rubrique présente des instructions étape par étape sur la façon de toorun un flux de travail de rédaction complète à l’aide d’Azure Media Services Explorer (AMSE) et Azure Media Redactor visualiseur (outil open source).

Hello **Azure Media Redactor** Pack d’administration est actuellement en version préliminaire. Il est disponible dans toutes les régions Azure publiques, ainsi que dans les centres de données de Chine et du Gouvernement des États-Unis. Cette version préliminaire est actuellement disponible gratuitement. Dans la version actuelle de hello, il existe une limite de 10 minutes sur la longueur de vidéo traitée.

Pour plus d’informations, consultez [ce](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) blog.

## <a name="azure-media-services-explorer-workflow"></a>Worfkflow d’Azure Media Services Explorer

Hello tooget de façon plus simple main Redactor est l’outil AMSE toouse hello open source sur github. Vous pouvez exécuter un workflow simplifié via **combinées** mode si vous ne devez accéder à toohello annotation json ou hello face jpg images.

### <a name="download-and-setup"></a>Téléchargement et configuration

1. Télécharger l’outil hello AMSE [ici](https://github.com/Azure/Azure-Media-Services-Explorer).
1. Ouvrez une session dans tooyour compte Media Services à l’aide de votre clé de service.

    tooobtain hello nom de compte et les informations de clé, accédez toohello [portail Azure](https://portal.azure.com/) et sélectionnez votre compte AMS. Sélectionnez Paramètres > Clés. windows de clés gérer Hello affiche le nom du compte hello et les clés primaires et secondaires hello s’affiche. Copiez les valeurs de nom de compte hello et de clé primaire de hello.

![Rédaction de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough001.png)

### <a name="first-pass--analyze-mode"></a>Premier passage - Mode d’analyse

1. Chargez votre fichier multimédia via Ressource -> Charger, ou par un glisser -déplacer. 
1. Cliquez avec le bouton droit de la souris et traitez votre fichier multimédia en utilisant 	Analytique multimédia –> Azure Media Redactor –> Mode Analyze. 


![Rédaction de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough002.png)

![Rédaction de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough003.png)

sortie de Hello inclut un fichier json d’annotations avec les données d’emplacement face, ainsi que jpg de chaque police détecté. 

![Rédaction de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough004.png)

###<a name="second-pass--redact-mode"></a>Second passage – Mode de rédaction

1. Téléchargez votre toohello élément multimédia vidéo d’origine, la sortie à partir de la première phase de hello et définie comme un élément multimédia principal. 

    ![Rédaction de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough005.png)

2. (Facultatif) Télécharger un fichier de « Dance_idlist.txt » qui inclut une liste de saut de ligne délimité de hello ID que vous souhaitez tooredact. 

    ![Rédaction de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough006.png)

3. (Facultatif) Effectuer n’importe quel fichier de annotations.json toohello modifications, comme augmenter hello des limites de la zone englobante. 
4. Cliquez avec le bouton droit sur hello élément multimédia de sortie à partir de la première phase de hello hello Redactor et sélectionnez Exécuter avec hello **Redact** mode. 

    ![Rédaction de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough007.png)

5. Télécharger ou partager hello finale rédigé actif. 

    ![Rédaction de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough008.png)

##<a name="azure-media-redactor-visualizer-open-source-tool"></a>Outil open source Azure Media Redactor Visualizer

Une open source [outil de visualiseur](https://github.com/Microsoft/azure-media-redactor-visualizer) est développeurs toohelp conçue en cours de démarrage avec le format d’annotations hello avec l’analyse et à l’aide de la sortie de hello.

Une fois que vous clonez le dépôt hello, dans le projet de commande toorun hello, vous devez toodownload FFMPEG à partir de leurs [site officiel](https://ffmpeg.org/download.html).

Si vous êtes un développeur de la tentative de tooparse hello données d’annotation JSON, recherchez à l’intérieur de Models.MetaData exemples de code d’exemple.

### <a name="set-up-hello-tool"></a>Configurer les outils de hello

1.  Téléchargez et générer l’ensemble de la solution hello. 

    ![Rédaction de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough009.png)

2.  Téléchargez FFMPEG [ici](https://ffmpeg.org/download.html). Ce projet a été développé à l’origine avec la version be1d324 (04-10-2016) avec une liaison statique. 
3.  Copiez ffmpeg.exe et ffprobe.exe toohello même dossier de sortie en tant que AzureMediaRedactor.exe. 

    ![Rédaction de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough010.png)

4. Exécutez AzureMediaRedactor.exe. 

### <a name="use-hello-tool"></a>Utilisez l’outil hello

1. Traiter les données vidéo dans votre compte Azure Media Services avec hello Redactor du Pack d’administration sur le mode d’analyse. 
2. Télécharger le fichier vidéo d’origine de hello et sortie hello Hello rédaction - analyser le travail. 
3. Exécutez l’application du visualiseur hello et choisissez les fichiers hello ci-dessus. 

    ![Rédaction de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough011.png)

4. Affichez un aperçu de votre fichier. Sélectionnez qui fait face vous aimeriez tooblur via encadré hello sur hello droite. 
    
    ![Rédaction de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough012.png)

5.  champ de texte Hello bas met à jour dont l’image de hello ID. Créez un fichier appelé « idlist.txt » avec ces ID sous forme de liste délimitée par un saut de ligne. 

    >[!NOTE]
    > Hello idlist.txt doivent être enregistrés au format ANSI. Vous pouvez utiliser le bloc-notes toosave au format ANSI.
    
6.  Télécharger ce fichier à toohello élément multimédia de sortie de l’étape 1. Télécharger hello actif d’origine toothis vidéo ainsi et définir comme principal. 
7.  Exécuter le travail de rédaction sur cet élément multimédia avec « Redact » en mode tooget hello rédigé vidéo finale. 

## <a name="next-steps"></a>Étapes suivantes 

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Liens connexes
[Vue d’ensemble d’Azure Media Services Analytics](media-services-analytics-overview.md)

[Démonstrations Azure Media Analytics](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

[Annonce de Face Redaction pour Azure Media Analytics](https://azure.microsoft.com/blog/azure-media-redactor/)
