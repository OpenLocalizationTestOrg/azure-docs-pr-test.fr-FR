---
title: "aaaMultiple d’entrée des fichiers et des propriétés de composant avec l’encodeur Premium - Azure | Documents Microsoft"
description: "Cette rubrique explique comment toouse setRuntimeProperties toouse entrée plusieurs fichiers et passer le processeur multimédia de données personnalisé toohello Workflow d’encodeur multimédia Premium."
services: media-services
documentationcenter: 
author: xpouyat
manager: cfowler
editor: 
ms.assetid: 7fb35bdd-9891-4401-a65b-ef3cc8190e8a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: xpouyat;anilmur;juliako
ms.openlocfilehash: e14d10fbf9669e0b88e5ba1c519f1ba5e0bafdd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-multiple-input-files-and-component-properties-with-premium-encoder"></a>Utilisation de plusieurs fichiers d’entrée et propriétés du composant avec Premium Encoder
## <a name="overview"></a>Vue d'ensemble
Il existe des scénarios dans lesquels vous devrez peut-être toocustomize propriétés du composant, spécifiez l’élément XML de liste contenu ou envoyer plusieurs fichiers d’entrée lorsque vous soumettez une tâche avec hello **Workflow d’encodeur multimédia Premium** processeur multimédia. Voici quelques exemples :

* Superposition vidéo de texte et en définissant la valeur de texte de hello (par exemple, date du jour hello) lors de l’exécution pour chaque vidéo d’entrée.
* Personnalisation de hello Clip liste XML (toospecify de source d’un ou plusieurs fichiers, avec ou sans limitation, etc.).
* Recouvrir une image de logo sur vidéo d’entrée de hello tandis que hello vidéo est encodée.
* Encodage de plusieurs langues audio.

toolet hello **Workflow d’encodeur multimédia Premium** savez que vous modifiez certaines propriétés dans le flux de travail hello lorsque vous créez la tâche hello ou que vous envoyez plusieurs fichiers d’entrée, vous avez une chaîne de configuration qui contient toouse  **setRuntimeProperties** et/ou **transcodeSource**. Cette rubrique explique comment toouse les.

## <a name="configuration-string-syntax"></a>Syntaxe de chaîne de configuration
tooset de chaîne de configuration Hello Bonjour encodage tâche utilise un document XML qui ressemble à ceci :

```xml
<?xml version="1.0" encoding="utf-8"?>
<transcodeRequest>
  <transcodeSource>
  </transcodeSource>
  <setRuntimeProperties>
    <property propertyPath="Media File Input/filename" value="VideoFileName.mp4" />
  </setRuntimeProperties>
</transcodeRequest>
```

Hello Voici le code hello c# qui lit un fichier de configuration XML hello, mettez-le à jour avec hello du nom de fichier vidéo et le passe toohello tâche dans un projet :

```c#
string premiumConfiguration = ReadAllText(@"D:\home\site\wwwroot\Presets\SetRuntime.xml").Replace("VideoFileName", myVideoFileName);

// Declare a new job.
IJob job = _context.Jobs.Create("Premium Workflow encoding job");

// Get a media processor reference, and pass tooit hello name of hello 
// processor toouse for hello specific task.
IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

// Create a task with hello encoding details, using a string preset.
ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                              processor,
                              premiumConfiguration,
                              TaskOptions.None);

// Specify hello input assets
task.InputAssets.Add(workflow); // workflow asset
task.InputAssets.Add(video); // video asset with multiple files

// Add an output asset toocontain hello results of hello job. 
// This output is specified as AssetCreationOptions.None, which 
// means hello output asset is not encrypted. 
task.OutputAssets.AddNew("Output asset", AssetCreationOptions.None);
```

## <a name="customizing-component-properties"></a>Personnalisation des propriétés du composant
### <a name="property-with-a-simple-value"></a>Propriété avec une valeur simple
Dans certains cas, il est utile toocustomize une propriété de composant avec le fichier de flux de travail hello qui est en train de toobe exécutée par le Workflow d’encodeur multimédia Premium.

Supposons que vous conçu un flux de travail que le texte superpositions sur vos vidéos, le texte hello (par exemple, date du jour hello) est supposé toobe ensemble lors de l’exécution. Pour cela, en envoyant toobe de texte hello définissez en tant que hello nouvelle valeur de propriété de texte hello du composant de superposition hello hello tâche de codage. Vous pouvez utiliser ce mécanisme toochange autres propriétés d’un composant dans le flux de travail hello (par exemple hello position ou les couleurs de superposition de hello, hello de vitesse de transmission de l’encodeur de hello AVC, etc..).

**setRuntimeProperties** est toooverride utilisé une propriété dans les composants de flux de travail hello hello.

Exemple :

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="MyInputVideo.mp4" />
      <property propertyPath="/primarySourceFile" value="MyInputVideo.mp4" />
      <property propertyPath="Optional Text Overlay/Text tooImage Converter/text" value="Today is Friday hello 13th of May, 2016"/>
  </setRuntimeProperties>
</transcodeRequest>
```

### <a name="property-with-an-xml-value"></a>Propriété avec une valeur XML
encapsuler des tooset une propriété qui attend une valeur XML, à l’aide de `<![CDATA[ and ]]>`.

Exemple :

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

> [!NOTE]
> Vérifiez que pas tooput chariot retournent juste après `<![CDATA[`.

### <a name="propertypath-value"></a>Valeur propertyPath
Dans les exemples précédents hello, hello propertyPath était « / du fichier multimédia/nom de fichier d’entrée » ou « / inactiveTimeout » ou « clipListXml ».
Il s’agit, en général, nom hello du composant de hello, puis nom hello de propriété de hello. Hello chemin d’accès peut avoir des niveaux plus ou moins, tel que « / primarySourceFile » (hello propriété étant à la racine hello hello de flux de travail) ou « / vidéo/opacité de traitement/graphique » (car hello superposition est dans un groupe).    

toocheck hello chemin d’accès au nom de propriété, utilisez bouton d’action hello située juste à côté de chaque propriété. Vous pouvez cliquer sur ce bouton d’action et sélectionner **Modifier**. Cette opération affiche vous hello réelle de nom de propriété de hello et immédiatement au-dessus d’elle, hello d’espace de noms.

![Action/Modifier](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture6_actionedit.png)

![Propriété](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture7_viewproperty.png)

## <a name="multiple-input-files"></a>Fichiers d’entrée multiples
Chaque tâche que vous envoyez toohello **Workflow d’encodeur multimédia Premium** nécessite deux composants :

* Bonjour tout d’abord un est un *actif du flux de travail* qui contient un fichier de flux de travail. Vous pouvez concevoir des fichiers de flux de travail à l’aide de hello [le Concepteur de flux de travail](media-services-workflow-designer.md).
* Hello second est un *multimédia* qui contient des fichiers de support hello que vous souhaitez tooencode.

Lorsque vous envoyez plusieurs toohello de fichiers de support **Workflow d’encodeur multimédia Premium** hello suivant des contraintes d’encodeur, applique :

* Tous les supports hello fichiers doivent être hello même *multimédia*. L’utilisation de plusieurs éléments multimédias n’est pas prise en charge.
* Vous devez définir le fichier primaire de hello dans cet élément multimédia Media (dans l’idéal, il s’agit de hello principal fichier vidéo hello encodeur est demandé tooprocess).
* Il s’agit des données de configuration nécessaires toopass inclut hello **setRuntimeProperties** et/ou **transcodeSource** processeur de toohello d’élément.
  * **setRuntimeProperties** est la propriété de nom de fichier utilisé toooverride hello ou une autre propriété dans les composants de flux de travail hello hello.
  * **transcodeSource** est utilisé toospecify hello contenu XML de liste de découpage.

Connexions dans le flux de travail hello :

* Si vous utilisez un ou plusieurs composants d’entrée de fichier de média et que vous prévoyez de toouse **setRuntimeProperties** toospecify hello du nom de fichier, puis ne se connectent pas hello fichier principal composant pin toothem. Assurez-vous qu’il n’existe aucune connexion entre objet du fichier primaire hello et hello Media fichier que les entrées.
* Si vous préférez toouse Clip liste XML et un composant de Source de média, puis vous pouvez connecter les deux ensemble.

![Aucune connexion à partir du fichier Source principal tooMedia fichier d’entrée](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture0_nopin.png)

*Il n’existe aucune connexion à partir du fichier primaire de hello tooMedia détecté (s) du fichier d’entrée si vous utilisez la propriété de nom de fichier setRuntimeProperties tooset hello.*

![Connexion à partir de la liste XML tooClip liste Source](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture1_pincliplist.png)

*Vous pouvez connecter la liste XML tooMedia Source et utiliser transcodeSource.*

### <a name="clip-list-xml-customization"></a>Personnalisation du fichier XML de liste de séquences
Vous pouvez spécifier hello XML de liste de découpage dans un flux de travail hello lors de l’exécution à l’aide de **transcodeSource** dans la configuration de hello chaîne XML. Cela requiert épingler le hello XML de liste de découpage toobe connecté Source de média toohello composant dans le flux de travail hello.

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <transcodeSource>
      <clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>video-part1.mp4</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>video-part1.mp4</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
      </clipList>
    </transcodeSource>
    <setRuntimeProperties>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

Si vous souhaitez toouse de /primarySourceFile toospecify cette sortie de hello tooname propriété fichiers à l’aide de « Expressions », nous vous recommandons de passer hello Clip liste XML en tant que propriété *après* propriété /primarySourceFile de hello, tooavoid Liste des images ayant hello être remplacée par le paramètre de /primarySourceFile hello.

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="c:\temp\start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>c:\temp\start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>c:\temp\start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

Avec découpage précis de la trame supplémentaire :

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <trim>
              <inPoint fps="25">00:00:05:24</inPoint>
              <outPoint fps="25">00:00:10:24</outPoint>
            </trim>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <trim>
              <inPoint fps="25">00:00:05:24</inPoint>
              <outPoint fps="25">00:00:10:24</outPoint>
            </trim>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

## <a name="example-1--overlay-an-image-on-top-of-hello-video"></a>Exemple 1 : Superposer une image sur hello vidéo

### <a name="presentation"></a>Présentation
Envisagez un exemple dans lequel vous souhaitez toooverlay une image de logo sur vidéo d’entrée de hello tandis que hello vidéo est encodée. Dans cet exemple, vidéo d’entrée de hello est nommé « Microsoft_HoloLens_Possibilities_816p24.mp4 » et le logo de hello est nommé « logo.png ». Vous devez exécuter hello comme suit :

* Créer un composant de flux de travail avec le fichier de flux de travail de hello (voir hello exemple suivant).
* Créer une ressource multimédia, qui contient deux fichiers : MyInputVideo.mp4 comme hello fichier primaire et MyLogo.png.
* Envoyer un toohello tâche multimédia de Workflow d’encodeur multimédia Premium ressources du processeur par hello ci-dessus d’entrée et spécifier des hello suivant de chaîne de configuration.

Configuration :

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="/primarySourceFile" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

Dans l’exemple hello ci-dessus, hello le nom de fichier vidéo de hello est envoyé toohello entrée de fichier de média composant hello primarySourceFile propriété. nom de Hello du fichier de logo hello est envoyé tooanother entrée de fichier de média qui est le composant de superposition graphique toohello connecté.

> [!NOTE]
> nom de fichier vidéo Hello est envoyée toohello primarySourceFile propriété. Hello raison à cela est toouse cette propriété dans le flux de travail hello pour la génération du nom de fichier de sortie correcte hello à l’aide d’Expressions, par exemple.

### <a name="step-by-step-workflow-creation"></a>Procédure de création de workflow pas à pas
Voici hello étapes toocreate un workflow qui utilise deux fichiers comme entrée : une vidéo et une image. Il sera superposer les images hello hello vidéo.

Ouvrez **Concepteur de flux de travail** et sélectionnez **Fichier** > **Nouvel espace de travail** > **Plan de transcodage**.

nouveau flux de travail Hello montre trois éléments :

* Fichier source principal
* Fichier XML de liste de séquences
* Fichier/élément multimédia de sortie  

![Nouveau workflow d’encodage](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture9_empty.png)

*Nouveau workflow d’encodage*

Dans le fichier de média d’entrée de commande tooaccept hello commencez par ajouter un composant Media fichier d’entrée. tooadd un flux de travail toohello du composant, regardez dans la zone de recherche du référentiel hello et faites glisser d’entrée de hello souhaité sur le volet de concepteur hello.

Ensuite, ajoutez toobe de fichier vidéo hello utilisée pour la conception de votre flux de travail. Par conséquent, les toodo sur le volet d’arrière-plan hello dans le Concepteur de flux de travail et recherchez propriété du fichier Source principal hello sur le volet de droite propriété hello. Cliquez sur icône du dossier hello et sélectionnez le fichier vidéo approprié de hello.

![Primary Source File](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture10_primaryfile.png)

*Primary Source File*

Ensuite, spécifiez le fichier vidéo de hello dans le composant d’entrée de fichier de média hello.   

![Source Media File Input](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture11_mediafileinput.png)

*Source Media File Input*

Dès que cette opération est effectuée, composant de support, fichier d’entrée hello inspecter le fichier de hello et remplir ses codes confidentiels tooreflect hello fichier de sortie il inspecté.

étape suivante de Hello est tooadd un tooRec.709 espace de couleur « Updater de Type de données vidéo » toospecify hello. Ajouter un « vidéo Format convertisseur » qui a le type de disposition/disposition tooData = PLANAIRE Configurable. Cela convertira hello flux vidéo tooa format qui peut être considéré comme une source de composant de superposition hello.

![Video Data Type Updater et Format Converter](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter.png)

*Video Data Type Updater et Format Converter*

![Type de disposition = Planaire configurable](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter2.png)

*Le type de disposition est Planaire configurable*

Ensuite, ajoutez un composant de la superposition vidéo et se connecter hello (non compressé) vidéo broche toohello (non compressé) vidéo broche d’entrée de fichier de média hello.

Ajouter un autre support de fichier d’entrée (fichier de logo tooload hello), cliquez sur ce composant et renommez-le trop « Support fichier d’entrée Logo », puis sélectionnez une image (un fichier .png par exemple) dans la propriété de fichier hello. Se connecter hello image non compressés broche toohello image non compressés broche de superposition de hello.

![Composant Overlay et source du fichier d’image](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture13_overlay.png)

*Composant Overlay et source du fichier d’image*

Si vous souhaitez que la position de hello toomodify du logo hello vidéo de hello (par exemple, vous pourriez tooposition à 10 pour cent sur les haut hello coin inférieur gauche de vidéo de hello), désactivez case à cocher « Entrée manuelle » hello. Pour cela, car vous utilisez un composant de segment de recouvrement toohello du fichier de logo entrée de fichier de média tooprovide hello.

![Position de superposition](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture14_overlay_position.png)

*Position de superposition*

tooencode hello flux vidéo tooH.264, ajoutez hello encodeur de vidéo AVC et l’aire du Concepteur de composants toohello encodeur AAC. Connecter des codes confidentiels hello.
Définissez encodeur AAC de hello et sélectionnez la Conversion de Format Audio/présélection : 2.0 (L, R).

![Encodeurs audio et vidéo](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture15_encoders.png)

*Encodeurs audio et vidéo*

Ajoutez maintenant hello **ISO Mpeg-4 multiplexeur** et **fichier de sortie** composants et se connecter à des codes confidentiels hello comme indiqué.

![MP4 Multiplexer et File Output](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture16_mp4output.png)

*MP4 Multiplexer et File Output*

Vous devez tooset hello nom hello fichier de sortie. Cliquez sur hello **fichier de sortie** composant et modifier l’expression hello pour le fichier de hello :

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_withoverlay.mp4

![Nom de sortie du fichier](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture17_filenameoutput.png)

*Nom de sortie du fichier*

Vous pouvez exécuter des flux de travail hello localement toocheck qu’elle s’exécute correctement.

Une fois terminé, vous pouvez l’exécuter dans Azure Media Services.

Tout d’abord, préparez un élément multimédia dans Azure Media Services avec deux fichiers : les fichiers vidéo hello et logo de hello. Pour cela, à l’aide des API hello .NET ou REST. Également procéder à l’aide de hello portail Azure ou [Azure Media Services Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).

Ce didacticiel vous montre comment les ressources toomanage avec AMSE. Il existe tooan actif de deux façons tooadd fichiers :

* Créez un dossier local, copiez des fichiers de hello deux et faites glisser hello dossier toohello **Asset** onglet.
* Télécharger le fichier vidéo de hello comme composant, afficher des informations de ressource hello, accédez de fichiers (onglet) toohello et télécharger un fichier supplémentaire (logo).

> [!NOTE]
> Assurez-vous que tooset un fichier primaire actif d’hello (fichier vidéo principal hello).

![Fichiers d’élément multimédia dans AMSE](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture18_assetinamse.png)

*Fichiers d’élément multimédia dans AMSE*

Sélectionnez hello actif et choisissez tooencode avec l’encodeur Premium. Télécharger les flux de travail hello et sélectionnez-le.

Cliquez sur le processeur toohello données hello bouton toopass et ajoutez hello XML tooset hello runtime propriétés suivantes :

![Premium Encoder dans AMSE](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture19_amsepremium.png)

*Premium Encoder dans AMSE*

Ensuite, copiez les données XML suivantes de hello. Vous avez besoin de nom de hello toospecify de fichier vidéo de hello pour hello entrée de fichier de média et primarySourceFile. Spécifiez le nom hello hello du nom de fichier pour le logo de hello trop.

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="/primarySourceFile" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

![setRuntimeProperties](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture20_amsexmldata.png)

*setRuntimeProperties*

Si vous utilisez toocreate du Kit de développement .NET hello et exécuter la tâche hello, ces données XML toobe passé en tant que chaîne de configuration hello.

```c#
public ITask AddNew(string taskName, IMediaProcessor mediaProcessor, string configuration, TaskOptions options);
```

Une fois le travail de hello terminée, fichier hello MP4 Bonjour sortie asset affiche le segment de recouvrement hello !

![Recouvrement sur hello vidéo](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture21_resultoverlay.png)

*Recouvrement sur hello vidéo*

Vous pouvez télécharger le workflow exemple hello [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).

## <a name="example-2--multiple-audio-language-encoding"></a>Exemple 2 : Encodage de plusieurs langues audio

Vous trouverez un exemple de workflow d’encodage de plusieurs langues audio dans [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).

Ce dossier contient un exemple de workflow qui peut être utilisé tooencode une ressource de fichiers MXF fichier tooa multiples MP4 avec plusieurs pistes audio.

Ce flux de travail suppose que ce fichier MXF hello contient une piste audio ; des pistes audio Hello supplémentaires doivent être passés en tant que fichiers audio distincts (WAV ou MP4...).

tooencode, procédez comme suit :

* Créer un élément multimédia Media Services avec hello et fichier MXF hello Audio (fichiers 0 too18 audio).
* Assurez-vous que ce fichier MXF hello est défini comme un fichier primaire.
* Créer une tâche et une tâche à l’aide du processeur d’encodeur de flux de travail Premium hello. Utilisez le workflow hello fourni (MultiMP4-1080p-19audio-v1.workflow).
* Passer la tâche de hello setruntime.xml données toohello (si vous utilisez l’Explorateur Azure Media Services, utilisation (bouton) « passer le flux de travail toohello de données xml » hello).
  * Mettez à jour hello données toospecify hello fichier correct pour les langues et les noms de balises XML.
  * flux de travail Hello comporte des éléments audio nommés 1 Audio tooAudio 18.
  * RFC5646 est pris en charge pour la balise de langue hello.

```xml
<?xml version="1.0" encoding="utf-16"?>
<transcodeRequest>
  <setRuntimeProperties>
    <property propertyPath="Media File Input Video/filename" value="MainVideo.mxf" />
    <property propertyPath="Language/language_code" value="en" />
    <property propertyPath="/primarySourceFile" value="MainVideo.mxf" />
    <property propertyPath="Audio 1/Media File Input/filename" value="french-audio.wav" />
    <property propertyPath="Audio 1/Language/language_code" value="fr" />
    <property propertyPath="Audio 2/Media File Input/filename" value="german-audio.wav" />
    <property propertyPath="Audio 2/Language/language_code" value="de" />
    <property propertyPath="Audio 3/Media File Input/filename" value="japanese-audio.wav" />
    <property propertyPath="Audio 3/Language/language_code" value="ja" />
  </setRuntimeProperties>
</transcodeRequest>
```

* actif de Hello encodé contiendra des pistes audio de langue multiples et ces pistes doivent être sélectionnés dans Azure Media Player.

## <a name="see-also"></a>Voir aussi
* [Présentation de l’encodage Premium dans Azure Media Services](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)
* [Comment toouse Premium encodage dans Azure Media Services](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)
* [Encodage de contenu à la demande avec Azure Media Services](media-services-encode-asset.md#media-encoder-premium-workflow)
* [Codecs et formats de Media Encoder Premium Workflow](media-services-premium-workflow-encoder-formats.md)
* [Exemples de fichiers de workflow](https://github.com/AzureMediaServicesSamples/Encoding-Presets/tree/master/VoD/MediaEncoderPremiumWorkfows)
* [Outil Azure Media Services Explorer](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
