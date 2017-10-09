---
title: "didacticiels de Workflow d’encodeur multimédia Premium aaaAvanced"
description: "Ce document contient des procédures pas à pas qui montrent comment tooperform avancé des tâches de Workflow d’encodeur multimédia Premium et également comment toocreate de workflows complexes avec le Concepteur de flux de travail."
services: media-services
documentationcenter: 
author: xstof
manager: cfowler
editor: 
ms.assetid: 1ba52865-b4a8-4ca0-ac96-920d55b9d15b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: christoc;xpouyat;juliako
ms.openlocfilehash: 641bd1be3bd795b5e138fa7ffdf299ff6710904e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-media-encoder-premium-workflow-tutorials"></a>Didacticiels de workflows avancés Media Encoder Premium
## <a name="overview"></a>Vue d'ensemble
Ce document contient des procédures pas à pas qui montrent comment les flux de travail toocustomize avec **le Concepteur de flux de travail**. Vous pouvez trouver hello les fichiers de flux de travail réelle [ici](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).  

## <a name="toc"></a>Table des matières
Hello rubriques suivantes est traitée :

* [Encodage du fichier MXF au format MP4 à débit binaire unique](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)
  * [Démarrage d’un nouveau workflow](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_start_new)
  * [À l’aide de hello entrée de fichier de média](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_file_input)
  * [Inspection des flux multimédias](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_streams)
  * [Ajout d’un encodeur vidéo pour la génération de fichiers MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_file_generation)
  * [Les flux de données audio encodage hello](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio)
  * [Multiplexage des flux audio et vidéo dans un conteneur de fichiers MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio_and_fideo)
  * [L’écriture du fichier MP4 hello](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_writing_mp4)
  * [Création d’un élément multimédia Media Services à partir du fichier de sortie hello](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_asset_from_output)
  * [Hello du test terminé localement les flux de travail](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_test)
* [Encodage du fichier MXF en fichiers MP4 multidébit avec l’empaquetage dynamique](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)
  * [Ajout d’une ou plusieurs sorties MP4 supplémentaires](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_more_outputs)
  * [Noms de sortie de fichier hello configuration](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_conf_output_names)
  * [Ajout d’une piste audio distincte](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_audio_tracks)
  * [Ajout de hello. Fichier SMIL ISM](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_ism_file)
* [Encodage du fichier MXF en fichiers MP4 multidébit : plan optimisé](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4)
  * [Tooenhance de vue d’ensemble du flux de travail](#workflow-overview-to-enhance)
  * [Conventions d’appellation de fichiers](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_file_naming)
  * [Propriétés du composant de publication sur la racine du flux de travail hello](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_publishing)
  * [Utilisation des valeurs de propriété publiées pour les noms de fichiers de sortie générés](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_output_files)
* [Ajout d’une sortie de miniatures toomultibitrate MP4](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4)
  * [Flux de travail vue d’ensemble tooadd miniatures](#workflow-overview-to-add-thumbnails-to)
  * [Ajout d’un encodage JPG](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4__with_jpg)
  * [Conversion de l’espace colorimétrique](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_color_space)
  * [Miniatures de hello en écriture](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_writing_thumbnails)
  * [Détection des erreurs dans un workflow](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_errors)
  * [Worflow terminé](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_finish)
* [Découpage temporel du fichier de sortie MP4 multidébit](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim)
  * [Toostart de vue d’ensemble du flux de travail ajout d’ajustement](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_start)
  * [À l’aide de hello découpage de flux de données](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_use_stream_trimmer)
  * [Worflow terminé](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_finish)
* [Présentation de hello composant de script](media-services-media-encoder-premium-workflow-tutorials.md#scripting)
  * [Écriture de scripts dans un workflow : Hello World](media-services-media-encoder-premium-workflow-tutorials.md#scripting_hello_world)
* [Découpage par images du fichier de sortie MP4 multidébit](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim)
  * [Géomètre toostart vue d’ensemble Ajout d’ajustement](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_start)
  * [À l’aide de hello XML de liste de découpage](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clip_list)
  * [Modification de la liste de découpage hello à partir d’un composant de script](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_modify_clip_list)
  * [Ajout d’une propriété de commodité ClippingEnabled](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clippingenabled_prop)

## <a id="MXF_to_MP4"></a>Encodage du fichier MXF au format MP4 à débit binaire unique
Dans cette procédure pas à pas, nous allons créer un fichier .MP4 à débit binaire unique avec des données audio encodées en AAC-HE à partir d’un fichier d’entrée .MXF.

### <a id="MXF_to_MP4_start_new"></a>Démarrage d’un nouveau workflow
Ouvrez Workflow Designer et sélectionnez « Fichier » > « Nouvel espace de travail » > « Plan de transcodage ».

nouveau flux de travail Hello affiche les 3 éléments :

* Fichier source principal
* Fichier XML de liste de séquences
* Fichier/élément multimédia de sortie  

![Nouveau workflow d’encodage](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-transcode-blueprint.png)

*Nouveau workflow d’encodage*

### <a id="MXF_to_MP4_with_file_input"></a>À l’aide de hello entrée de fichier de média
Dans l’ordre tooaccept notre fichier multimédia d’entrée, une commence par ajout d’un composant Media fichier d’entrée. tooadd un flux de travail toohello du composant, regardez dans la zone de recherche du référentiel hello et faites glisser d’entrée de hello souhaité sur le volet de concepteur hello. Cela pour hello Media fichier d’entrée et se connecter hello fichier Source principal composant toohello nom de fichier d’entrée code confidentiel de hello Media fichier d’entrée.

![Composant Media File Input connecté](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-input.png)

*Composant Media File Input connecté*

Avant que nous pouvons faire beaucoup d’autres, nous aurons besoin tout d’abord le fichier d’exemple aux tooindicate le Concepteur de flux de travail toohello nous aimerions toouse toodesign avec notre flux de travail. toodo par conséquent, cliquez sur arrière-plan du volet de concepteur hello et rechercher pour la propriété du fichier Source principal hello sur le volet de droite propriété hello. Cliquez sur icône du dossier hello et flux de travail hello hello sélectionnez souhaité pour fichier tootest avec. Dès que cette opération est effectuée, composant de support, fichier d’entrée hello inspecter le fichier de hello et renseigner ses broches de sortie tooreflect fichier hello qu'il inspecté.

![Composant Media File Input renseigné](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-populated-media-file-input.png)

*Composant Media File Input renseigné*

Alors que cela spécifie avec le type de données, nous souhaiterions toowork avec, il n’indique pas encore où doit atteindre la sortie de hello encodé. Similaire hello toohow principal fichier Source a été configuré, à présent configurer hello propriété de la Variable de dossier de sortie, juste en dessous.

![Propriétés d’entrée et de sortie configurées](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configured-io-properties.png)

*Propriétés d’entrée et de sortie configurées*

### <a id="MXF_to_MP4_streams"></a>Inspection des flux multimédias
Souvent, il est souhaité tooknow aspect que des flux de données hello transite par le flux de travail hello. tooinspect un flux de données à tout moment dans le flux de travail hello, cliquez simplement sur une sortie ou une broche d’entrée sur un des composants de hello. Dans ce cas, essayez de cliquer sur une broche de sortie hello vidéo non compressé à partir de notre fichier multimédia d’entrée. Une boîte de dialogue s’ouvre et permet la vidéo de tooinspect hello sortant.

![Broche de sortie de l’inspection hello vidéo non compressé](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-inspecting-uncompressed-video-output.png)

*Broche de sortie de l’inspection hello vidéo non compressé*

Dans notre cas, nous savons par exemple que nous avons affaire à une entrée 1920 x 1080 à 24 images par seconde en échantillonnage 4:2:2 pour une vidéo d’un peu moins de 2 minutes.

### <a id="MXF_to_MP4_file_generation"></a>Ajout d’un encodeur vidéo pour la génération de fichiers MP4
Notez que notre composant Media File Input comporte maintenant une broche de sortie Uncompressed Video et plusieurs broches de sortie Uncompressed Audio. Dans l’ordre tooencode hello vidéo entrant, nous avons besoin d’un composant de codage - dans ce cas pour la génération. Fichiers MP4.

tooencode hello tooH.264 de flux vidéo, ajouter l’aire du Concepteur de composant toohello encodeur de vidéo AVC hello. Ce composant utilise un flux vidéo non compressé comme entrée et génère un flux vidéo AVC compressé sur sa broche de sortie.

![Encodeur AVC non connecté](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-avc-encoder.png)

*Encodeur AVC non connecté*

Ses propriétés déterminent comment l’encodage hello exactement. Nous allons avoir un aperçu des hello plus importants :

* Largeur de sortie et la hauteur de la sortie : ils déterminent la résolution de la vidéo de hello encodé hello. Dans le cas présent, partons sur une résolution de 640 x 360.
* Fréquence d’images : lorsque toopassthrough ensemble il sera juste adoptent la fréquence d’images source hello, il est possible toooverride comme vous le voyez. Notez que cette conversion de fréquence d’images n’est pas compensée en mouvement.
* Niveau et un profil : ils déterminent le profil de hello AVC et le niveau. tooconveniently obtenir plus d’informations sur les différents niveaux de hello et les profils, cliquez sur icône du point d’interrogation hello sur le composant d’encodeur de vidéo AVC hello et la page d’aide hello affiche plus de détails sur chacun des niveaux de hello. Pour notre exemple, passons avec profil principal au niveau 3.2 (valeur par défaut de hello).
* Mode de contrôle du débit et débit binaire (kbit/s) : dans notre scénario, nous allons opter pour un débit binaire constant (CBR) à 1 200 kbit/s.
* Format vidéo : il s’agit sur hello VUI (informations sur la facilité d’utilisation vidéo) qui est écrites dans le flux de données hello H.264 (informations côté qui peuvent être utilisées par un affichage de décodeur tooenhance hello, mais non essentiel toocorrectly décoder) :
* NTSC (standard aux États-Unis ou au Japon, avec un débit de 30 images par seconde)
* PAL (standard en Europe, avec un débit de 25 images par seconde)
* Mode de taille de groupe d’images : nous allons ici configurer une taille de groupe d’images fixe avec un intervalle de clé de 2 secondes et des groupes d’images fermés. Cela garantit la compatibilité avec hello qu'empaquetage dynamique Azure Media Services fournit.

toofeed notre encodeur AVC, source broche de sortie vidéo non compressé hello hello Media fichier d’entrée composant toohello vidéo non compressé broche d’entrée à partir de l’encodeur de hello AVC.

![Encodeur AVC connecté](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-avc-encoder.png)

*Encodeur AVC principal connecté*

### <a id="MXF_to_MP4_audio"></a>Les flux de données audio encodage hello
À ce stade, nous avons codées vidéo mais hello le flux audio non compressé d’origine doit toujours toobe compressé. Pour cela, nous allons passer avec AAC codage par hello composant AAC encodeur (Dolby). Ajouter toohello le flux de travail.

![Encodeur AVC non connecté](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-aac-encoder.png)

*Encodeur AAC non connecté*

Maintenant il existe une incompatibilité : il est uniquement une seule non compressée audio broche d’entrée à partir de hello AAC encodeur lors de la plus probable hello fichier d’entrée de support dispose de deux différents décompressé flux audio disponible : un pour hello gauche du canal et l’autre pour hello Oui. (soit 6 canaux dans le cas d’un son surround). Il est donc pas possible toodirectly Branchez audio de hello à partir de la source d’entrée de fichier de média hello encodeur audio AAC de hello. composant AAC Hello attend un flux audio « entrelacé » soi-disant : un flux unique qui possède ces deux hello canaux gauche et hello droite entrelacés avec eux. Une fois que nous savons à partir de notre fichier du média source les pistes audio sur quelle position dans la source de hello, nous pouvons générer correctement ce flux audio entrelacé avec hello assignés positions haut-parleur de gauche et droite.

Tout d’abord un pouvez toogenerated un flux entrelacé de canaux audio de sources hello requis. composant d’ENTRELACEUR de flux Audio Hello gère cela pour nous. Ajouter des flux de travail toohello et connecter les sorties audio hello de hello entrée de fichier de média dans ce.

![Composant Audio Stream Interleaver connecté](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-audio-stream-interleaver.png)

*Composant Audio Stream Interleaver connecté*

Maintenant que nous avons un flux audio entrelacé, nous n’a pas spécifier où les haut-parleurs tooassign hello gauche ou droite de positions. Dans commande toospecify cela, nous pouvons exploiter hello haut-parleur de la Position assigne.

![Ajout d’un composant Speaker Position Assigner](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-speaker-position-assigner.png)

*Ajout d’un composant Speaker Position Assigner*

Configurer hello haut-parleur de la Position assigne pour une utilisation avec un flux d’entrée stéréo via un filtre de présélection d’encodeur de « Custom » et hello canal prédéfini appelé « 2.0 (L, R) ». (Cela permet d’affecter hello haut-parleur gauche position toochannel 1 et hello haut-parleur droit position toochannel 2.)

Connectez sortie hello d’entrée de toohello hello haut-parleur de la Position assigne de hello AAC encodeur. Ensuite, indiquez toowork de AAC encodeur hello avec un « 2.0 (L, R) » prédéfini de canal, afin qu’il sache toodeal avec audio stéréo en tant qu’entrée.

### <a id="MXF_to_MP4_audio_and_fideo"></a>Multiplexage des flux audio et vidéo dans un conteneur de fichiers MP4
Nous pouvons maintenant capturer notre flux vidéo encodé en AVC et notre flux audio encodé en AAC dans un conteneur de fichiers .MP4. processus de Hello de mélange de différents flux en un seul est appelé « multiplexage » (ou « muxing »). Dans ce cas, nous allons entrelacement hello flux audio et hello vidéo dans une seule cohérente. Package de fichiers MP4. composant Hello qui coordonne d’un. MP4 conteneur est appelé hello multiplexeur ISO MPEG-4. Ajouter une aire du concepteur toohello et connecter hello AVC vidéo encodeur et entrées de tooits AAC encodeur hello.

![Multiplexeur MPEG4 connecté](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-mpeg4-multiplexer.png)

*Multiplexeur MPEG4 connecté*

### <a id="MXF_to_MP4_writing_mp4"></a>L’écriture du fichier MP4 hello
Lorsque vous écrivez un fichier de sortie, le composant de sortie du fichier hello est utilisé. Nous pouvons nous connecter cette sortie toohello Hello multiplexeur ISO MPEG-4, afin que sa sortie obtient écrit toodisk. toodo, connecter hello conteneur (MPEG-4) sortie pin toohello écriture broche d’entrée de fichier de sortie de hello.

![Composant File Output connecté](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-file-output.png)

*Composant File Output connecté*

Hello de nom de fichier qui sera utilisé est déterminé par hello propriété de fichier. Si cette propriété peut être codé en dur les tooa valeur donnée, probablement un souhaiteront tooset par le biais d’une expression à la place.

flux de travail toohave hello déterminer automatiquement la sortie de hello propriété à partir d’une expression de nom de fichier, cliquez sur le nom de fichier hello bouton suivant toohello (icône de dossier suivant toohello). À partir de hello menu déroulant, puis sélectionnez « Expression ». Éditeur d’expression hello s’affiche. Effacer tout d’abord le contenu de hello de l’éditeur de hello.

![Éditeur d’expressions vide](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-empty-expression-editor.png)

*Éditeur d’expressions vide*

Éditeur d’expression Hello permet tooenter toute valeur littérale, combiné avec une ou plusieurs variables. Les variables commencent par le symbole de dollar. Lorsque vous atteignez la clé de $ hello, éditeur de hello affiche une zone de liste déroulante avec un choix de variables disponibles. Dans le cas présent, nous allons utiliser une combinaison de variable de répertoire de sortie hello et variable de nom de fichier d’entrée de base hello :

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}.MP4

![Éditeur d’expressions renseigné](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-expression-editor.png)

*Éditeur d’expressions renseigné*

> [!NOTE]
> Dans l’ordre toosee voir un fichier de sortie de votre travail d’encodage dans Azure, vous devez fournir une valeur dans l’éditeur d’expression hello.
>
>

Lorsque vous confirmez l’expression de hello en appuyant sur OK, fenêtre des propriétés hello aperçu toowhat valeur hello fichier propriété résout à ce stade.

![L’expression du fichier résout le répertoire de sortie](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-expression-resolves-output-dir.png)

*L’expression du fichier résout le répertoire de sortie*

### <a id="MXF_to_MP4_asset_from_output"></a>Création d’un élément multimédia Media Services à partir du fichier de sortie hello
Pendant que nous avons écrit un fichier de sortie MP4, nous devons encore tooindicate que ce fichier appartienne toohello de sortie actif, les services de support générera suite à l’exécution de ce flux de travail. fin de toothis, nœud d’élément multimédia sortie fichier hello sur le canevas de flux de travail hello est utilisé. Tous les fichiers entrants dans ce nœud fera partie d’actifs d’Azure Media Services qui en résulte hello.

Se connecter hello sortie du fichier composant toohello fichier/élément multimédia de sortie composant toofinish hello du flux de travail.

![Worflow terminé](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow.png)

*Worflow terminé*

### <a id="MXF_to_MP4_test"></a>Hello du test terminé localement les flux de travail
tootest hello flux de travail local, d’accès au bouton de lecture hello dans la barre d’outils hello haut hello. Lorsque le flux de travail hello terminé son exécution, inspecter la sortie hello généré dans le dossier de sortie hello configuré. Vous verrez hello fin de fichier de sortie MP4 qui a été encodée à partir des fichiers de source d’entrée MXF hello.

## <a id="MXF_to_MP4_with_dyn_packaging"></a>Encodage du fichier MXF en fichiers MP4 multidébit avec l’empaquetage dynamique
Dans cette procédure pas à pas, nous allons créer un ensemble de fichiers .MP4 multidébit avec un flux audio encodé en AAC à partir d’un seul fichier d’entrée .MXF.

Quand une sortie d’élément multimédia débits est souhaitée pour une utilisation en association avec les fonctionnalités d’empaquetage dynamique hello offertes par Azure Media Services, plusieurs fichiers MP4 alignés GOP de chacun une autre vitesse de transmission et la résolution devez toobe généré. toodo hello donc [MXF de codage dans une vitesse de transmission unique MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) procédure pas à pas fournit un bon point de départ.

![Démarrage du workflow](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow.png)

*Démarrage du workflow*

### <a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Ajout d’une ou plusieurs sorties MP4 supplémentaires
Chaque fichier MP4 contenu dans l’élément multimédia Azure Media Services que nous avons généré prendra en charge des valeurs de débit binaire et de résolution différentes. Vous allez ajouter un ou plusieurs fichiers MP4 sortie fichiers toohello du flux de travail.

toomake que nous avons tous nos encodeurs vidéos créés avec hello les mêmes paramètres, ses tooduplicate mieux hello d’encodeur vidéo AVC déjà existants et configurer une autre combinaison de résolution et de la vitesse de transmission (nous allons ajouter l’un de 960 x 540 à 25 images par seconde à 2,5 Mbits/s). tooduplicate d’encodeur existants hello, copier et coller il sur l’aire du concepteur hello.

Connexion de la broche de sortie vidéo non compressé hello Hello entrée de fichier de média dans notre nouveau composant AVC.

![Deuxième encodeur AVC connecté](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-avc-encoder-connected.png)

*Deuxième encodeur AVC connecté*

Maintenant adapter configuration hello pour notre toooutput encodeur de nouveau AVC 960 x 540 à Mbits/s 2,5. (Pour cela, utilisez les propriétés « largeur de sortie », « hauteur de sortie » et « débit binaire (Kbit/s) »).

Fonction nous souhaitons asset résultant de hello toouse avec mise en package dynamique Azure Media Services, hello point de terminaison de diffusion en continu doit toobe capable de générer à partir de ces fichiers MP4 des fragments de TLS/fragmenté MP4/DASH qui sont exactement aligné tooeach autre de façon que les clients qui sont de commutation entre différents débits binaires obtiennent une seule expérience sans heurts continue audio et vidéo. toomake qui se produisent, nous devons tooensure que, dans les propriétés des deux encodeurs AVC hello hello taille GOP (« groupe d’images ») pour les deux fichiers MP4 a la valeur too2 secondes, ce qui peuvent être effectuées par :

* définir la taille de GOP hello Mode de dimensionnement GOP tooFixed et
* Hello Key Frame intervalle tootwo en secondes.
* également définir hello GOP IDR contrôle tooClosed GOP tooensure tous les GOP est permanent sur leurs propres sans dépendances

toomake notre toounderstand pratique de flux de travail, renommer les encodeur AVC première hello trop « encodeur de vidéo AVC 640 x 360 Kbits/s 1200 » et hello deuxième encodeur de AVC » l’encodeur vidéo AVC 960 x 540 Kbits/s 2500 ».

Ajoutez maintenant un deuxième multiplexeur ISO MPEG-4 et un deuxième composant File Output. Se connecter hello multiplexeur toohello nouvel AVC encodeur et assurez-vous que sa sortie est dirigée dans hello fichier de sortie. Puis également vous connecter de nouveau de toohello de sortie du codeur audio AAC hello entrée de multiplexeur. Hello, fichier de sortie à son tour peut ensuite être tooadd de nœud de fichier/élément multimédia de sortie toohello connecté il toohello Services multimédia qui sera créé.

![Deuxièmes composants Muxer et File Output connectés](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-muxer-file-output-connected.png)

*Deuxièmes composants Muxer et File Output connectés*

Pour la compatibilité avec l’empaquetage dynamique d’Azure Media Services, configurer la durée ou au nombre de tooGOP hello du multiplexeur Mode de segment et définir GOP hello par segment too1. (Il doit s’agir par défaut de hello).

![Modes bloc du multiplexeur](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-muxer-chunk-modes.png)

*Modes bloc du multiplexeur*

Remarque : vous souhaiterez toorepeat ce processus pour toute vitesse de transmission et de la résolution combinaisons de toohave ajouté une sortie d’élément multimédia toohello.

### <a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Noms de sortie de fichier hello configuration
Nous avons plus d’une ressource en sortie toohello Ajout de fichier unique. Cela fournit un hello vraiment besoin toomake pour chacun des hello les noms de fichiers de sortie fichiers diffèrent les uns des autres et peut-être même appliquent une convention d’affectation de noms de fichier afin qu’il devienne clair hello nom de fichier que vous avez affaire à.

Nom de sortie de fichier peut être contrôlée par des expressions dans le Concepteur de hello. Ouvrez le volet des propriétés pour un des composants de la sortie de fichier hello hello et ouvrir l’éditeur d’expression hello pour hello propriété de fichier. Notre premier fichier de sortie a été configuré via l’expression suivante de hello (consultez Didacticiel hello pour allant [à débit binaire unique MXF tooa MP4 sortie](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)) :

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}.MP4

Cela signifie que votre nom de fichier est déterminée par deux variables : hello sortie Active toowrite hello et en nom base du fichier source. ancienne de Hello est exposé en tant que propriété sur la racine du flux de travail hello et hello ce dernier est déterminée par les fichiers entrants hello. Notez ce répertoire de sortie hello est ce que vous utilisez pour le test local ; Cette propriété sera remplacée par le moteur de flux de travail hello lorsque le flux de travail hello est exécutée par le processeur d’un média basé sur le cloud hello dans Azure Media Services.
toogive à la fois une sortie cohérente d’affectation de noms de fichiers de notre sortie, de modification hello fichiers tout d’abord une expression d’affectation de noms à :

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

et hello ensuite à :

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_960x540_2.MP4

Exécutez un test intermédiaire exécuter toomake que les deux fichiers de sortie MP4 sont correctement générés.

### <a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Ajout d’une piste audio distincte
Comme nous verrons plus tard lorsque nous générons une toogo de fichier .ism avec ses fichiers de sortie MP4, nous doit disposer d’un fichier MP4 audio uniquement en tant que piste audio de hello notre diffusion adaptative en continu. toocreate ce fichier, ajouter un flux de travail supplémentaires muxer toohello (multiplexeur ISO-MPEG-4) et se connecter broche de sortie de l’encodeur hello AAC avec son code confidentiel d’entrée pour la piste 1.

![Ajout du multiplexeur audio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-added.png)

*Ajout du multiplexeur audio*

Créer un troisième fichier composant toooutput hello sortant le flux de sortie à partir de hello muxer et configurer l’expression d’affectation de noms de fichier hello en tant que :

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_128kbps_audio.MP4

![Création du composant File Output par le multiplexeur audio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-creating-file-output.png)

*Création du composant File Output par le multiplexeur audio*

### <a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Ajout de hello. Fichier SMIL ISM
Pour toowork d’empaquetage dynamique hello en combinaison avec les deux fichiers MP4 les fichiers (et hello MP4 audio uniquement) dans notre élément multimédia Media Services, nous devons également un fichier manifeste (également appelé fichier de « SMIL » : synchronisé Multimedia Integration Language). Ce fichier indique tooAzure Media Services quels fichiers MP4 sont disponibles pour l’empaquetage dynamique et de ces tooconsider pour la diffusion audio hello. Le fichier manifeste associé à un ensemble de fichiers MP4 à un seul flux audio se présente généralement comme suit :

    <?xml version="1.0" encoding="utf-8" standalone="yes"?>
    <smil xmlns="http://www.w3.org/2001/SMIL20/Language">
      <head>
        <meta name="formats" content="mp4" />
      </head>
      <body>
        <switch>
          <video src="H264_1900kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_1300kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_900kbps_AAC_und_ch2_96kbps.mp4" />
          <audio src="AAC_ch2_96kbps.mp4" title="AAC_und_ch2_96kbps" />
        </switch>
      </body>
    </smil>

fichier .ism de Hello contient au sein d’une instruction switch, un tooeach de référence de hello MP4 vidéo des fichiers individuels, et en outre les fichiers audio toothose également un (ou plus) fait référence à tooan MP4 contenant uniquement des données audio de hello.

Génération du fichier manifeste hello pour notre ensemble de MP4 est possible via un composant appelé hello « AMS manifeste Writer ». toouse, faites glisser sur l’aire de hello et connecter hello broches de sortie « Écriture terminée » à partir de toohello de composants de la sortie de fichier trois hello Writer de manifeste AMS d’entrée. Vérifiez que sortie de hello tooconnect de hello Writer de manifeste AMS toohello fichier/élément multimédia de sortie.

Comme avec nos autres composants de sortie de fichier, configurez hello nom de sortie du fichier .ism avec une expression :

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_manifest.ism

Notre flux de travail terminé ressemble à hello ci-dessous :

![Flux de travail MP4 terminé MXF toomultibitrate](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-mxf-to-multibitrate-mp4-workflow.png)

*Flux de travail MP4 terminé MXF toomultibitrate*

## <a id="MXF_to__multibitrate_MP4"></a>Encodage du fichier MXF en fichiers MP4 multidébit : plan optimisé
Bonjour [procédure pas à pas de flux de travail précédent](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) nous l’avons vu comment un élément multimédia d’entrée unique MXF peut être converti en un élément multimédia de sortie avec des fichiers MP4 à plusieurs débits, un fichier MP4 audio uniquement et un fichier manifest à utiliser conjointement avec Azure Media Services d’empaquetage dynamique.

Cette procédure pas à pas affiche comment certaines des aspects de hello peuvent être améliorés et rendue plus pratique.

### <a id="MXF_to_multibitrate_MP4_overview"></a>Tooenhance de vue d’ensemble du flux de travail
![Tooenhance du flux de travail Multibitrate MP4](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-enhance.png)

*Tooenhance du flux de travail Multibitrate MP4*

### <a id="MXF_to__multibitrate_MP4_file_naming"></a>Conventions d’appellation de fichiers
Dans le flux de travail précédent hello que nous avons spécifié une expression simple en tant que base de hello pour générer les noms de fichier de sortie. Nous avons des valeurs en double si : tous les composants de fichier de sortie individuelle de hello hello telle expression spécifiée.

Par exemple, notre composant de sortie de fichier pour le premier fichier de vidéo hello est configuré avec cette expression :

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

Pour la sortie de la deuxième de hello vidéo, nous disposons d’une expression telle que :

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_960x540_2.MP4

Pourquoi ne pas rendre tout cela plus clair, juste et pratique en évitant ces doublons et en renforçant les possibilités de configuration ? Heureusement, nous pouvons : les fonctionnalités d’expression du concepteur hello en association avec les propriétés personnalisées de toocreate possibilité hello sur notre racine du flux de travail donne une couche supplémentaire de commodité.

Supposons que nous allons lecteur configuration du nom de fichier à partir de débits binaires de hello de fichiers MP4 hello. Ces débits binaires que nous allons visent tooconfigure dans un centre placer (sur hello racine notre graphique), à partir d’où ils seront d’accès tooconfigure et lecteur nom génération du fichier. toodo, nous allons commencer par la propriété de vitesse de transmission hello à partir de deux racine AVC encodeurs toohello notre flux de travail, de publication pour qu’elle devienne accessible depuis les deux racine hello ainsi que les encodeurs hello AVC. (même si cette propriété s’affiche à deux endroits différents, il n’y a qu’une seule valeur sous-jacente).

### <a id="MXF_to__multibitrate_MP4_publishing"></a>Propriétés du composant de publication sur la racine du flux de travail hello
Ouvrir les encodeur AVC première hello, atteindre la propriété de débit binaire (Kbits/s) toohello et à partir de la liste déroulante de hello choisissez Publier.

![Propriété de vitesse de transmission hello publication](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-bitrate-property.png)

*Propriété de vitesse de transmission hello publication*

Configurer hello publier la boîte de dialogue toopublish toohello racine de notre graphique de flux de travail, avec un nom publié de « video1bitrate » et un nom complet explicite de « Vitesse de transmission vidéo 1 ». Configurez un nom de groupe personnalisé appelé « Streaming Bitrates » et appuyez sur Publier.

![Propriété de vitesse de transmission hello publication](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-bitrate-property.png)

*Boîte de dialogue de publication pour la propriété de débit binaire*

Répétez ces étapes hello identiques pour la propriété de vitesse de transmission hello Hello deuxième encodeur de AVC et nommez-la « video2bitrate » avec un nom d’affichage de « Vitesse de transmission vidéo 2 », Bonjour personnalisé de groupe « Débits binaires de diffusion en continu ».

Si nous avons maintenant examiner les propriétés racine du flux de travail hello, nous allons voir notre groupe personnalisé avec hello deux propriétés publiées s’affichent. Les deux sont reflétant la valeur hello de leur transmission d’encodeur AVC respectif.

![Propriétés de débit binaire publiées sur la racine du workflow](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-bitrate-props-on-workflow-root.png)

Chaque fois que nous souhaitons tooaccess ces propriétés à partir du code ou à partir d’une expression, nous pouvons le faire comme suit :

* à partir de code inline à partir d’un composant juste sous la racine de hello : node.getPropertyAsString('.. / video1bitrate', la valeur null)
* dans une expression : ${ROOT_video1bitrate}

Nous allons terminer le groupe de « Débits binaires de diffusion en continu » hello en publiant notre bitrate piste audio sur celui-ci. Dans Propriétés de hello de hello AAC encodeur, recherchez le paramètre de vitesse de transmission hello et sélectionnez Publier dans tooit suivant de liste déroulante hello. Publier racine toohello du graphique hello avec le nom « audio1bitrate » et afficher le nom « Vitesse de transmission Audio 1 » au sein de notre groupe personnalisé « Débits binaires de diffusion en continu ».

![Boîte de dialogue de publication pour le débit audio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-audio-bitrate.png)

*Boîte de dialogue de publication pour le débit audio*

![Propriétés vidéo et audio générées à la racine](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-resulting-video-and-audio-props-on-root.png)

*Propriétés vidéo et audio générées à la racine*

Notez que la modification de ces trois valeurs également reconfigure et modifications hello valeurs sur les composants respectifs hello qu’ils sont liés par (et où publiées à partir de).

### <a id="MXF_to__multibitrate_MP4_output_files"></a>Utilisation des valeurs de propriété publiées pour les noms de fichiers de sortie générés
Au lieu de coder en dur nos noms de fichier généré, nous pouvons de maintenant modifier votre expression de nom de fichier sur chacun des toorely de composants de la sortie de fichier hello sur les propriétés de vitesse de transmission hello que nous venez de publier sur la racine du graphique hello. À partir de notre première sortie de fichier, de trouver la propriété de fichier hello et modifier l’expression hello comme suit :

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video1bitrate}kbps.MP4

différents paramètres de cette expression Hello sont accessibles et entrés en appuyant sur le signe dollar de hello clavier hello tandis que dans la fenêtre d’expression hello. Un des paramètres disponibles de hello est notre propriété video1bitrate que nous avons publié précédemment.

![Accès aux paramètres dans une expression](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-accessing-parameters-within-an-expression.png)

*Accès aux paramètres dans une expression*

Hello même pour la sortie de fichier hello pour notre vidéo deuxième :

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video2bitrate}kbps.MP4

et pour la sortie du fichier audio uniquement hello :

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_audio1bitrate}bps_audio.MP4

Si nous modifions maintenant le débit hello des hello fichiers vidéo ou audio, encodeur respectifs de hello est reconfiguré et convention de nom de fichier basé sur la vitesse de transmission hello sera honorée automatique toutes les.

## <a id="thumbnails_to__multibitrate_MP4"></a>Ajout d’une sortie de miniatures toomultibitrate MP4
À partir d’un flux de travail qui génère [une sortie à plusieurs débits MP4 à partir d’une entrée de MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), nous allons maintenant l’examiner dans Ajout d’une sortie toohello de miniatures.

### <a id="thumbnails_to__multibitrate_MP4_overview"></a>Flux de travail vue d’ensemble tooadd miniatures
![Toostart de flux de travail Multibitrate MP4 à partir de](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-start-from.png)

*Toostart de flux de travail Multibitrate MP4 à partir de*

### <a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>Ajout d’un encodage JPG
cœur de Hello de notre la génération de miniatures sera composant JPG encodeur hello toooutput en mesure des fichiers JPG.

![Encodeur JPG](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-jpg-encoder.png)

*Encodeur JPG*

Nous ne pouvons pas toutefois vous connecter directement notre flux vidéo non compressé à partir de hello entrée de fichier de média dans un encodeur JPG hello. Au lieu de cela, il attend toobe transmettre des frames individuels. Cette opération, nous pouvons faire via un composant de vidéo Frame porte hello.

![Connexion d’un encodeur de frame porte toohello JPG](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-frame-gate-to-jpg-encoder.png)

*Connexion d’un encodeur de frame porte toohello JPG*

porte de frame Hello une seule fois chaque secondes ou les cadres autant autorise un toopass images vidéo. Hello hello et intervalle de décalage horaire avec lequel cela se produit est configurable dans les propriétés de hello.

![Propriétés du composant Video Frame Gate](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-video-frame-gate-properties.png)

*Propriétés du composant Video Frame Gate*

Créez une miniature de chaque minute en définissant le mode de hello tooTime (secondes) et hello too60 d’intervalle.

### <a id="thumbnails_to__multibitrate_MP4_color_space"></a>Conversion de l’espace colorimétrique
Pendant qu’il peut sembler logique à la fois des codes confidentiels vidéo non compressée de la porte de frame hello et hello entrée de fichier de média peuvent maintenant être connectés, vous obtenez un avertissement si nous pour cela.

![Erreur de l’espace colorimétrique d’entrée](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-input-color-space-error.png)

*Erreur de l’espace colorimétrique d’entrée*

Il s’agit, car hello dans quelle couleur informations sont représentées dans notre flux d’origine brute non compressée vidéo, en provenance de notre MXF, est différent de quel hello JPG encodeur attend. Plus spécifiquement, un dite « espace de couleurs » de « RVB » ou « Gris » est attendu tooflow dans. Cela signifie que flux vidéo entrant de ce hello vidéo Frame de porte devez toohave une conversion appliquée concernant son espace de couleurs en premier.

Faites glisser sur hello de flux de travail hello convertisseur d’espace de couleurs - Intel et connectez-la porte de frame tooour.

![Connexion d’un convertisseur d’espace colorimétrique](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-color-space-convertor.png)

*Connexion d’un convertisseur d’espace colorimétrique*

Dans la fenêtre de propriétés hello, choisissez entrée hello RVB 24 à partir de la liste de présélection hello.

### <a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Miniatures de hello en écriture
Différents à partir de notre vidéo MP4, hello encodeur JPG composant produira et plusieurs fichiers. Dans toodeal d’ordre avec cette, un composant de Writer de fichier JPG scène recherche peut être utilisé : elle prend les miniatures JPG entrants hello et les écrire, chaque nom de fichier qui est suivie d’un nombre différent. (nombre de hello généralement indiquant hello différents/unités de secondes dans le flux hello hello miniature a été dessiné à partir de).

![Présentation de hello Writer de fichier JPG scène recherche](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer.png)

*Présentation de hello Writer de fichier JPG scène recherche*

Configurer la propriété de chemin d’accès du dossier de sortie hello avec expression de hello : ${ROOT_outputWriteDirectory}

et hello propriété préfixe de nom de fichier :

    ${ROOT_sourceFileBaseName}_thumb_

préfixe de Hello déterminent comment les fichiers de miniatures hello sont nommés. Est le suffixe à la position d’un nombre indiquant hello du curseur dans le flux de hello.

![Propriétés du composant Scene Search JPG File Writer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer-properties.png)

*Propriétés du composant Scene Search JPG File Writer*

Connectez le nœud d’élément multimédia sortie fichier hello Writer de fichier JPG scène recherche toohello.

### <a id="thumbnails_to__multibitrate_MP4_errors"></a>Détection des erreurs dans un workflow
Se connecter entrée hello hello couleur espace convertisseur toohello brute non compressée sortie vidéo. Maintenant effectuer une série de flux de travail hello de tests locale. Il y a un flux de travail de fortes chances hello est soudainement arrêter l’exécution et indiquer avec un contour rouge sur le composant hello a rencontré une erreur :

![Erreur du convertisseur d’espace colorimétrique](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error.png)

*Erreur du convertisseur d’espace colorimétrique*

Cliquez sur l’icône « E » hello peu rouge dans hello coin supérieur droit de hello convertisseur d’espace de couleurs composant toosee quelle est la raison hello Échec de la tentative de codage hello.

![Boîte de dialogue d’erreur du convertisseur d’espace colorimétrique](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error-dialog.png)

*Boîte de dialogue d’erreur du convertisseur d’espace colorimétrique*

Il s’avère, comme vous pouvez le voir, que rec601 toobe pour notre conversion demandée de YUV tooRGB hello entrants espace de couleurs standard pour le convertisseur d’espace de couleurs hello. Apparemment, notre flux n’indique pas qu’il s’agit de la norme rec601 (Rec 601 est une norme d’encodage de signaux vidéo analogiques entrelacés sous forme de vidéo numérique. Elle spécifie une région active couvrant 720 échantillons de luminance et 360 échantillons de chrominance par ligne. système de codage de couleur de Hello est appelé parade 4:2:2.)

toofix, nous allons indiquer des métadonnées de hello de notre flux que nous manipulons rec601 contenu. toodo, nous allons utiliser un composant de mise à jour de Type de données vidéo, nous mettrons entre nos brut source et hello couleur espace composant de conversion. Cette mise à jour du type de données permet de propriétés de type pour la mise à jour manuelle de hello de certaines données vidéos. Configurer tooindicate un espace couleur Standard de « Rec 601 ». Cela entraîne un flux de hello tootag hello mise à jour de Type de données vidéo avec l’espace de couleurs « Rec 601 » hello s’il y a aucun espace colorimétrique encore définie. (Il ne remplace pas toutes les métadonnées existantes, sauf si la case à cocher du remplacement de hello a été activée.)

![Mise à jour de couleur espace Standard sur hello mise à jour du Type de données](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-update-color-space-standard-on-data-type.png)

*Mise à jour de couleur espace Standard sur hello mise à jour du Type de données*

### <a id="thumbnails_to__multibitrate_MP4_finish"></a>Worflow terminé
Maintenant que notre notre flux de travail est terminé, effectuez une autre série de tests toosee s’il satisfait.

![Flux de travail terminé pour la sortie MP4 multidébit avec miniatures](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-for-multi-mp4-thumbnails.png)

*Flux de travail terminé pour la sortie MP4 multidébit avec miniatures*

## <a id="time_based_trim"></a>Découpage temporel du fichier de sortie MP4 multidébit
À partir d’un flux de travail qui génère [une sortie à plusieurs débits MP4 à partir d’une entrée de MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), nous allons maintenant l’examiner en réduisant hello source vidéo basé sur un horodatage.

### <a id="time_based_trim_start"></a>Toostart de vue d’ensemble du flux de travail ajout d’ajustement
![Ajustement de flux de travail tooadd de démarrage](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow-to-add-trimming.png)

*Ajustement de flux de travail tooadd de démarrage*

### <a id="time_based_trim_use_stream_trimmer"></a>À l’aide de hello découpage de flux de données
composant de flux de données découpage Hello permet tootrim hello début et à la fin d’un flux d’entrée de base sur les informations de minutage (secondes, minutes,...). découpage de Hello ne prend pas en charge basée sur le frame de suppression.

![Composant Stream Trimmer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-stream-trimmer.png)

*Composant Stream Trimmer*

Au lieu de lier directement les encodeurs hello AVC et haut-parleur de la position assigne toohello entrée de fichier de média, nous mettrons entre ces découpage de flux hello. (Un pour les signaux vidéo hello et pour le signal audio entrelacée de hello).

![Insertion du composant Stream Trimmer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-put-stream-trimmer-in-between.png)

*Insertion du composant Stream Trimmer*

Permet de configurer le découpage de hello afin que nous traiterons uniquement vidéo et audio entre 15 et 60 secondes dans une vidéo de hello.

Accédez de propriétés toohello Hello découpage du flux vidéo et configurer l’heure de début (15 s) et les propriétés de l’heure de fin (60 s). Nous publierons toomake qu’à la fois notre découpage audio et vidéo est toujours configurée toohello même début et de fin des valeurs, ces racine toohello hello de flux de travail.

![Publication de la propriété d’heure de début à partir du composant Stream Trimmer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-start-time-from-stream-trimmer.png)

*Publication de la propriété d’heure de début à partir du composant Stream Trimmer*

![Boîte de dialogue des propriétés de publication pour l’heure de début](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-start-time.png)

*Boîte de dialogue des propriétés de publication pour l’heure de début*

![Boîte de dialogue des propriétés de publication pour l’heure de fin](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-end-time.png)

*Boîte de dialogue des propriétés de publication pour l’heure de fin*

Si nous avons maintenant inspecter racine hello notre flux de travail, les deux propriétés seront soigneusement affichée et peut être configuré à partir de là.

![Propriétés publiées disponibles sur la racine](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-properties-available-on-root.png)

*Propriétés publiées disponibles sur la racine*

Ouvrez les propriétés de rognage hello de découpage d’audio hello et configurer des heures de début et de fin d’une expression qui fait référence toohello publié les propriétés de la racine hello notre flux de travail.

Pour l’heure de début d’ajustement audio hello :

    ${ROOT_TrimmingStartTime}

et pour son heure de fin :

    ${ROOT_TrimmingEndTime}

### <a id="time_based_trim_finish"></a>Worflow terminé
![Worflow terminé](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-time-base-trimming.png)

*Worflow terminé*

## <a id="scripting"></a>Présentation de hello composant de script
Les composants sous forme de script peuvent exécuter des scripts arbitraires au cours des phases d’exécution de hello de notre flux de travail. Il existe quatre différents scripts qui peuvent être exécutés, chacun avec des caractéristiques spécifiques et leur propres sur place dans le cycle de vie de workflow hello :

* **commandScript**
* **realizeScript**
* **processInputScript**
* **lifeCycleScript**

documentation Hello Hello composant de script va plus en détail pour chacun des hello ci-dessus. Dans [hello suivants section](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), hello **realizeScript** composant de script est tooconstruct utilisé un fichier xml de liste de séquences volée hello lorsque hello workflow démarre. Ce script est appelé lors de l’installation de composant hello, ce qui se produit une seule fois dans son cycle de vie.

### <a id="scripting_hello_world"></a>Écriture de scripts dans un workflow : Hello World
Faites glisser un composant de l’objet d’un script sur l’aire du concepteur hello et renommez-le (par exemple, « SetClipListXML »).

![Ajout d’un composant de script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

*Ajout d’un composant de script*

Lorsque vous examinez les propriétés hello de hello composant de script, hello quatre types différents de script seront affiche, chaque script différents tooa configurable.

![Propriétés du composant de script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

*Propriétés du composant de script*

Désactivez hello processInputScript et ouvrir l’éditeur de hello pour hello realizeScript. Maintenant nous est configurés et prêt toostart de script.

Les scripts sont écrits en Groovy, un langage de script compilé de manière dynamique pour la plate-forme Java hello qui conserve la compatibilité avec Java. En fait, la plupart des codes Java sont considérés comme du code Groovy valide.

Nous allons écrire un script de sensationnelle simple hello world dans un contexte hello de notre realizeScript. Entrez les informations suivantes de hello dans l’éditeur de hello :

    node.log("hello world");

Exécutez maintenant une série de tests en local. Après cette exécution, inspecter (via l’onglet système hello hello composant de script) hello propriété de journaux.

![Sortie du journal Hello World](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output.png)

*Sortie du journal Hello World*

objet de nœud Hello nous appeler la méthode hello du journal, fait référence tooour actuel « nœud » ou un composant hello nous mettons scripts dans. Ainsi, chaque composant a les données de journalisation toooutput de capacité salutation, disponibles via l’onglet système de hello. Dans ce cas, nous sortie hello littéral de chaîne « hello world ». Toounderstand important ici est que cela peut s’avérer toobe un outil de débogage précieux, en vous fournissant des informations sur le script hello est en fait.

À partir de dans notre environnement de script, nous avons accès tooproperties avec d’autres composants. Procédez comme suit :

    //inspect current node:
    def nodepath = node.getNodePath();
    node.log("this node path: " + nodepath);

    //walking up tooother nodes:
    def parentnode = node.getParentNode();
    def parentnodepath = parentnode.getNodePath();
    node.log("parent node path: " + parentnodepath);

    //read properties from a node:
    def sourceFileExt = parentnode.getPropertyAsString( "sourceFileExtension", null );
    def sourceFileName = parentnode.getPropertyAsString("sourceFileBaseName", null);
    node.log("source file name with extension " + sourceFileExt + " is: " + sourceFileName);

Notre fenêtre journal permet de visualiser hello suivant :

![Sortie de journal pour l’accès aux chemins du nœud](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output2.png)

*Sortie de journal pour l’accès aux chemins du nœud*

## <a id="frame_based_trim"></a>Découpage par images du fichier de sortie MP4 multidébit
À partir d’un flux de travail qui génère [une sortie à plusieurs débits MP4 à partir d’une entrée de MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), nous allons maintenant l’examiner en réduisant hello source vidéo en fonction du frame.

### <a id="frame_based_trim_start"></a>Géomètre toostart vue d’ensemble Ajout d’ajustement
![Toostart de flux de travail ajout d’ajustement](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-workflow-start-adding-trimming-to.png)

*Toostart de flux de travail ajout d’ajustement*

### <a id="frame_based_trim_clip_list"></a>À l’aide de hello XML de liste de découpage
Dans tous les didacticiels précédents de flux de travail, nous avons utilisé le composant de fichier d’entrée de média hello en tant que source d’entrée vidéo. Pour ce scénario, nous utiliserons composant de Source de la liste hello à la place. Notez que cela ne doit pas être la méthode hello préféré de travail ; Utilisez uniquement hello Source de la liste lorsqu’il existe donc un toodo véritable raison (comme dans hello ci-dessous cas, où nous procédons à utiliser les fonctionnalités de suppression de liste de découpage hello).

tooswitch à partir de notre toohello d’entrée de fichier de média Clip liste Source, faites glisser de composant de Source de la liste de hello sur l’aire de conception hello et se connecter hello Clip liste pin toohello Clip liste XML nœud XML du Concepteur de flux de travail hello. Cela doit remplir hello Source de la liste des codes confidentiels de sortie, selon la vidéo d’entrée de tooour. Maintenant vous connecter les broches non compressée vidéo et Audio non compressé hello de hello hello Clip liste Source toohello respectifs AVC encodeurs et ENTRELACEUR de flux Audio. Supprimer hello entrée de fichier de média.

![Remplacé hello entrée de fichier de média avec hello Clip liste Source](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-replaced-media-file-with-clip-source.png)

*Remplacé hello entrée de fichier de média avec hello Clip liste Source*

composant de Source de la liste Hello prend comme entrée un « XML de liste de découpage ». Lorsque vous sélectionnez hello tootest de fichier source avec localement, ce xml de liste de découpage est rempli automatiquement pour vous.

![Propriété du fichier XML de liste de séquences automatiquement renseigné](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-auto-populated-clip-list-xml-property.png)

*Propriété du fichier XML de liste de séquences automatiquement renseigné*

Recherchez un peu plus toohello xml, voici comment il ressemble à :

![Boîte de dialogue de modification de la liste de séquences](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-edit-clip-list-dialog.png)

*Boîte de dialogue de modification de la liste de séquences*

Toutefois, cela ne reflète pas les fonctions hello hello clip liste XML. Une option que nous avons est tooadd un élément « Trim » sous la vidéo de hello et la source de l’audio, comme suit :

![Ajout d’une liste de découpage toohello élément trim](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-trim-element-to-clip-list.png)

*Ajout d’une liste de découpage toohello élément trim*

Si vous modifiez du code xml de liste de découpage hello comme ci-dessus et effectuez une série de tests locale, vous verrez la vidéo de hello été correctement supprimés entre 10 et 20 secondes dans une vidéo de hello.

Toowhat contraire se produit lorsque vous effectuez une exécution locale, bien que ce code xml de liste de séquences très même n’aurait pas hello même effet en cas d’application dans un flux de travail qui s’exécute dans Azure Media Services. Lorsque Azure Premium encodeur démarre, xml de liste de séquences hello est généré chaque fois, en fonction de l’encodage du hello hello fichier d’entrée le travail a été spécifié. Cela signifie que toutes les modifications sur hello xml sont malheureusement substituées.

xml de liste de séquences hello toocounter leur réinitialisation au démarrage d’une tâche de codage, nous pouvons générer de nouveau il hello volée juste après le début de hello de notre flux de travail. Ces actions personnalisées peuvent être exécutées via ce que l’on appelle un « composant de script ». Pour plus d’informations, consultez [présentation hello composant de script](media-services-media-encoder-premium-workflow-tutorials.md#scripting).

Faites glisser un composant de l’objet d’un script sur l’aire du concepteur hello et renommez-le trop « SetClipListXML ».

![Ajout d’un composant de script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

*Ajout d’un composant de script*

Lorsque vous examinez les propriétés hello de hello composant de script, hello quatre types différents de script seront affiche, chaque script différents tooa configurable.

![Propriétés du composant de script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

*Propriétés du composant de script*

### <a id="frame_based_trim_modify_clip_list"></a>Modification de la liste de découpage hello à partir d’un composant de script
Avant que nous pouvons réécrire xml de liste de séquences de hello est généré lors du démarrage du flux de travail, nous avons besoin de contenu et la propriété xml de toohave accès toohello liste de séquences. Pour cela, nous pouvons procéder de la manière suivante :

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: " + clipListXML);

![Liste de séquences entrantes consignée dans le journal](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-incoming-clip-list-logged.png)

*Liste de séquences entrantes consignée dans le journal*

Tout d’abord, nous devons un toodetermine moyen point à partir duquel jusqu'à quel point nous souhaitons tootrim hello vidéo. publication de cet utilisateur de moins technique toohello pratique de flux de travail hello, toomake racine toohello de deux propriétés de graphique de hello. toodo, cliquez avec le bouton droit sur aire du concepteur hello et sélectionnez « Ajouter une propriété » :

* Première propriété : « ClippingTimeStart » de type : « TIMECODE »
* Deuxième propriété : « ClippingTimeEND » de type : « TIMECODE »

![Boîte de dialogue Ajouter une propriété pour l’heure de début du découpage](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-start-time.png)

*Boîte de dialogue Ajouter une propriété pour l’heure de début du découpage*

![Propriétés de temps de découpage publiées sur la racine du workflow](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-time-props.png)

*Propriétés de temps de découpage publiées sur la racine du workflow*

Configurez les deux valeur appropriée de tooa de propriétés :

![Configurer hello extrait les propriétés de début et de fin](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configure-clip-start-end-prop.png)

*Configurer hello extrait les propriétés de début et de fin*

À partir de dans notre script, nous pouvons désormais accéder aux deux propriétés, comme suit :

    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    node.log("clipping start: " + clipstart);
    node.log("clipping end: " + clipend);

![Fenêtre de journal indiquant le début et la fin du découpage](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-show-start-end-clip.png)

*Fenêtre de journal indiquant le début et la fin du découpage*

Nous allons analyser des chaînes de code temporel hello dans un formulaire toouse plus pratique, à l’aide d’une expression régulière simple :

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);
    node.log("framerate end is: " + endframerate);

![Fenêtre de journal avec la sortie du code temporel analysé](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-output-parsed-timecode.png)

*Fenêtre de journal avec la sortie du code temporel analysé*

Avec ces informations à portée de main, nous pouvons maintenant modifier hello liste de séquences xml tooreflect hello et heures de fin des hello souhaité précis extrait de film de hello.

![Éléments trim tooadd de code de script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-trim-elements.png)

*Éléments trim tooadd de code de script*

Nous avons utilisé pour cela des opérations normales de manipulation de chaîne. xml de liste Hello obtenu image modifiée est réécrites toohello clipListXML propriété sur la racine du flux de travail hello via la méthode de « setProperty » hello. fenêtre de journal Hello après l’exécution d’un autre test nous indiquerait hello suivant :

![Liste des images qui en résulte hello de journalisation](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-result-clip-list.png)

*Liste des images qui en résulte hello de journalisation*

Effectuer un toosee de série de tests comment les flux vidéo et audio hello ont été réduits. Comme vous allez effectuer plus d’une série de tests avec des valeurs différentes pour les points de rognage hello, vous remarquerez que celles ne seront pas pris en compte toutefois ! raison Hello est ce concepteur hello, contrairement aux hello runtime Azure, ne pas remplacer xml de liste de séquences d’hello chaque exécution. Cela signifie qu’uniquement hello première fois que vous avez défini hello et l’extraction des points, cause hello xml tootransform, de tous les autres hello fois, notre clause guard (si (clipListXML.indexOf («<trim>») == -1)) empêche les flux de travail hello d’ajouter un autre découpage élément s’il existe déjà présent.

toomake notre flux de travail pratique tootest localement, nous meilleures ajouter du code de conservation de maison qui vérifie si un élément de découpage était déjà présent. Dans ce cas, vous pouvez le supprimer avant de continuer en modifiant le xml hello avec de nouvelles valeurs de hello. Au lieu d’utiliser des manipulations de chaîne simple, il est probablement plus sûre toodo grâce à l’objet réel xml de modèle d’analyse.

Avant que nous pouvons ajouter ce code Cependant, nous devrons tooadd qu'un nombre d’instructions d’importation à hello démarrer d’abord de notre script :

    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

Après cela, nous pouvons ajouter hello requis du code de nettoyage :

    //for local testing: delete any pre-existing trim elements from hello clip list xml by parsing hello xml into a DOM:
    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements,dom,XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
     //delete hello trim nodes:
    elementsToDelete.each{
        e -> e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

Ce code va juste au-dessus de point hello auquel nous ajoutons hello éléments toohello liste des séquences xml.

À ce stade, nous pouvons exécuter et modifier notre flux de travail que nous voulons que bien que les modifications de hello appliquées jamais de temps.    

### <a id="frame_based_trim_clippingenabled_prop"></a>Ajout d’une propriété de commodité ClippingEnabled
Comme vous toujours pouvez ajustement toohappen, nous allons terminer notre flux de travail en ajoutant un pratique indicateur booléen qui indique si nous voulons tooenable trimming / extrait.

Comme avant, publiez une nouvelle racine toohello de propriété de notre flux de travail appelé « ClippingEnabled » de type « BOOLEAN ».

![Publication d’une propriété activant le découpage](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-enable-clip.png)

*Publication d’une propriété activant le découpage*

Avec hello ci-dessous clause de garde simple, nous pouvons vérifier si la suppression est requise et décidez si la liste des images en tant que tel toobe modifié ou non.

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }


### <a id="code"></a>Code complet
    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: \n" + clipListXML);
    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);

    node.log("framerate end is: " + endframerate);

    //for local testing: delete any pre-existing trim elements
    //from hello clip list xml by parsing hello xml into a DOM:

    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements, dom, XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
    //delete hello trim nodes:
    elementsToDelete.each{ e ->
        e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }

    //add trim elements toocliplist xml
    if ( clipListXML.indexOf("<trim>") == -1 )
    {
        //trim video
        clipListXML = clipListXML.replace("<videoSource>","<videoSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\"" + endframerate +"\"> " + endtimecode +
            " </outPoint>\n </trim> \n");
        //trim audio
        clipListXML = clipListXML.replace("<audioSource>","<audioSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\""+ endframerate +"\">" +
            endtimecode + "</outPoint>\n </trim>\n");
        node.log( "clip list going out: \n" +clipListXML );
        node.setProperty("../clipListXml",clipListXML);
    }


## <a name="also-see"></a>Voir aussi
[Présentation de l’encodage Premium dans Azure Media Services](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)

[Comment tooUse Premium encodage dans Azure Media Services](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)

[Encodage de contenu à la demande avec Azure Media Services](media-services-encode-asset.md#media-encoder-premium-workflow)

[Codecs et formats de Media Encoder Premium Workflow](media-services-premium-workflow-encoder-formats.md)

[Exemples de fichiers de workflow](http://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows)

[Outil Azure Media Services Explorer](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
