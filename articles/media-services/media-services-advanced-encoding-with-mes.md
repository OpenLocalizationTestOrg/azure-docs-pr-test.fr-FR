---
title: "aaaPerform avancée en personnalisant MES Présélections d’encodage | Documents Microsoft"
description: "Cette rubrique montre comment tooperform avancée en personnalisant les présélections de tâches Media Encoder Standard de codage."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 2a4ade25-e600-4bce-a66e-e29cf4a38369
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: juliako
ms.openlocfilehash: 9caa68fafacaf51f91f0554c5bafe491928d8c77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="perform-advanced-encoding-by-customizing-mes-presets"></a>Effectuer un encodage avancé en personnalisant les présélections MES 

## <a name="overview"></a>Vue d'ensemble

Cette rubrique montre comment toocustomize Media Encoder Standard prédéfinis. Hello [encodage avec Media Encoder Standard à l’aide des paramètres prédéfinis personnalisés](media-services-custom-mes-presets-with-dotnet.md) rubrique indique comment toouse .NET toocreate est un encodage de tâches et d’une tâche qui exécute cette tâche. Une fois que vous personnalisez une présélection de tâche d’encodage approvisionnement hello Présélections personnalisées toohello. 

>[!NOTE]
>Si vous utilisez une présélection XML, vérifiez qu’ordre de hello toopreserve des éléments, comme indiqué dans les exemples XML ci-dessous (par exemple, KeyFrameInterval doit précéder SceneChangeDetection).
>

Dans cette rubrique, hello des paramètres prédéfinis personnalisés qui effectuent hello suivant les tâches d’encodage sont illustrées.

## <a name="support-for-relative-sizes"></a>Prise en charge des tailles relatives

Lors de la génération de miniatures, vous n’avez pas besoin tooalways spécifier la largeur de sortie et la hauteur en pixels. Vous pouvez les spécifier en pourcentages, dans la plage de hello [% 1, …, 100 %].

### <a name="json-preset"></a>Présélection JSON
    "Width": "100%",
    "Height": "100%"

### <a name="xml-preset"></a>Présélection XML
    <Width>100%</Width>
    <Height>100%</Height>

## <a id="thumbnails"></a>Génération de miniatures

Cette section montre comment toocustomize une présélection qui génère les miniatures. Hello présélection définie ci-dessous contient des informations sur la façon dont vous souhaitez que tooencode votre fichier ainsi que les informations nécessaires toogenerate miniatures. Vous pouvez prendre l’une des présélections MES hello documentées [cela](media-services-mes-presets-overview.md) section et ajoutez le code qui génère des miniatures.  

> [!NOTE]
> Hello **SceneChangeDetection** paramètre Bonjour suivant prédéfini ne peut être définie tootrue si vous codez tooa à débit binaire unique vidéo. Si vous codez débits tooa vidéo et définir **SceneChangeDetection** tootrue, l’encodeur de hello retourne une erreur.  
>
>

Pour plus d’informations sur le schéma, consultez [cette](media-services-mes-schema.md) rubrique.

Assurez-vous que tooreview hello [considérations](#considerations) section.

### <a id="json"></a>Présélection JSON
    {
      "Version": 1.0,
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": "true",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 4500,
              "MaxBitrate": 4500,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "ReferenceFrames": 3,
              "EntropyMode": "Cabac",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"

            }
          ],
          "Type": "H264Video"
        },
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "{Best}",
          "Type": "JpgImage"
        },
        {
          "PngLayers": [
            {
              "Type": "PngLayer",
              "Width": 640,
              "Height": 360,
            }
          ],
          "Start": "00:00:01",
          "Step": "00:00:10",
          "Range": "00:00:58",
          "Type": "PngImage"
        },
        {
          "BmpLayers": [
            {
              "Type": "BmpLayer",
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "10%",
          "Step": "10%",
          "Range": "90%",
          "Type": "BmpImage"
        },
        {
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        },
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "PngFormat"
          }
        },
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "BmpFormat"
          }
        },
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <a id="xml"></a>Présélection XML
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <SceneChangeDetection>true</SceneChangeDetection>
          <H264Layers>
            <H264Layer>
              <Bitrate>4500</Bitrate>
              <Width>1280</Width>
              <Height>720</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>4500</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
        <JpgImage Start="{Best}">
          <JpgLayers>
            <JpgLayer>
              <Width>640</Width>
              <Height>360</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
        <BmpImage Start="10%" Step="10%" Range="90%">
          <BmpLayers>
            <BmpLayer>
              <Width>640</Width>
              <Height>360</Height>
            </BmpLayer>
          </BmpLayers>
        </BmpImage>
        <PngImage Start="00:00:01" Step="00:00:10" Range="00:00:58">
          <PngLayers>
            <PngLayer>
              <Width>640</Width>
              <Height>360</Height>
            </PngLayer>
          </PngLayers>
        </PngImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <BmpFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <PngFormat />
        </Output>
      </Outputs>
    </Preset>

### <a name="considerations"></a>Considérations

Hello suivant considérations s’appliquent :

* Utilisez Hello des horodateurs explicite pour la plage de début/étape suppose que cette source d’entrée hello est 1 minute au moins.
* Les éléments Jpg/Png/BmpImage possèdent les attributs de chaîne Start, Step et Range, qui peuvent être interprétés comme suit :

  * Entiers non négatifs : nombre d’images, par exemple "Start": "120",
  * Durée toosource relatif si exprimée sous la forme %-suivi du suffixe, par exemple « Start » : « 15 % », ou
  * Horodatage, s’il est exprimé au format HH:MM:SS, par exemple « Start » : « 00:01:00 »

    Vous pouvez combiner et apparier les notations à votre guise.

    En outre, début prend également en charge une Macro spéciale : {meilleures}, qui tente de toodetermine hello premier « intéressantes » frame de contenu de hello Remarque : (étape et la plage sont ignorés lorsque le démarrage est défini trop {meilleures})
  * La configuration par défaut est « Start:{Best} ».
* Format de sortie doit toobe explicitement fourni pour chaque format d’Image : Jpg/Png/BmpFormat. Le cas échéant, MES correspond JpgVideo tooJpgFormat et ainsi de suite. OutputFormat introduit une nouvelle Macro spécifique codec d’image : {Index}, laquelle doit toobe présent (une fois et une seule fois) pour les formats de sortie d’image.

## <a id="trim_video"></a>Rognage d’une vidéo (extrait)
Cette section aborde les modification encodeur de hello prédéfinit tooclip ou rogner la vidéo d’entrée de hello où hello entrée est un fichier de ce que l'on appelle mezzanine ou à la demande. Hello encodeur peut également être utilisé tooclip ou supprimer un élément multimédia, qui est capturé ou à partir d’un flux en direct : hello détails de ce sont disponibles dans [ce billet de blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).

tootrim vos vidéos, vous pouvez effectuer les présélections MES hello documentées [cela](media-services-mes-presets-overview.md) section et modifier hello **Sources** élément (comme indiqué ci-dessous). valeur de Hello de StartTime doit toomatch hello des horodateurs absolu de la vidéo d’entrée de hello. Par exemple, si hello du premier frame de la vidéo d’entrée de hello a un horodateur de 12:00:10.000, StartTime doit être au moins 12:00:10.000 et supérieur. Dans l’exemple hello ci-dessous, nous supposons qu’entrée hello vidéo a un horodateur de début égale à zéro. **Sources** doivent être placés au début de hello hello prédéfini.

### <a id="json"></a>Présélection JSON
    {
      "Version": 1.0,
      "Sources": [
        {
          "StartTime": "00:00:04",
          "Duration": "00:00:16"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 3400,
              "MaxBitrate": 3400,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 2250,
              "MaxBitrate": 2250,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1500,
              "MaxBitrate": 1500,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1000,
              "MaxBitrate": 1000,
              "BufferWindow": "00:00:05",
              "Width": 640,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 650,
              "MaxBitrate": 650,
              "BufferWindow": "00:00:05",
              "Width": 640,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 400,
              "MaxBitrate": 400,
              "BufferWindow": "00:00:05",
              "Width": 320,
              "Height": 180,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

### <a name="xml-preset"></a>Présélection XML
tootrim vos vidéos, vous pouvez effectuer les présélections MES hello documentées [ici](media-services-mes-presets-overview.md) et modifier hello **Sources** élément (comme indiqué ci-dessous).

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source StartTime="PT4S" Duration="PT14S"/>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>3400</Bitrate>
              <Width>1280</Width>
              <Height>720</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>3400</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>2250</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>2250</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1500</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1500</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1000</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1000</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>650</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>650</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>400</Bitrate>
              <Width>320</Width>
              <Height>180</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>400</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>

## <a id="overlay"></a>Création d’une superposition

Hello Media Encoder Standard vous permet de toooverlay une image sur une vidéo existante. Actuellement, hello suivant les formats est pris en charge : png, jpg, gif et bmp. Bonjour présélection définie ci-dessous est un exemple de base d’une superposition vidéo.

En outre toodefining un fichier prédéfini, vous avez également toolet Media Services connaître le fichier d’élément multimédia de hello est l’image de superposition hello et le fichier est hello source vidéo sur lequel vous souhaitez l’image de hello toooverlay. fichier vidéo de Hello a toobe hello **principal** fichier.

Si vous utilisez .NET, ajoutez hello suivant deux fonctions toohello .NET exemple défini dans [cela](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) rubrique. Hello **UploadMediaFilesFromFolder** fonction télécharge les fichiers à partir d’un dossier (par exemple, BigBuckBunny.mp4 et Image001.png) et jeux hello fichier toobe hello principal fichier mp4 dans un élément multimédia de hello. Hello **EncodeWithOverlay** fonction utilise hello prédéfini fichier personnalisé qui a été passé à tooit (par exemple, hello prédéfini qui suit) toocreate hello tâche d’encodage.


    static public IAsset UploadMediaFilesFromFolder(string folderPath)
    {
        IAsset asset = _context.Assets.CreateFromFolder(folderPath, AssetCreationOptions.None);
    
        foreach (var af in asset.AssetFiles)
        {
            // hello following code assumes 
            // you have an input folder with one MP4 and one overlay image file.
            if (af.Name.Contains(".mp4"))
                af.IsPrimary = true;
            else
                af.IsPrimary = false;
    
            af.Update();
        }
    
        return asset;
    }

    static public IAsset EncodeWithOverlay(IAsset assetSource, string customPresetFileName)
    {
        // Declare a new job.
        IJob job = _context.Jobs.Create("Media Encoder Standard Job");
        // Get a media processor reference, and pass tooit hello name of hello 
        // processor toouse for hello specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(customPresetFileName);

        // Create a task
        ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input assets toobe encoded.
        // This asset contains a source file and an overlay file.
        task.InputAssets.Add(assetSource);

        // Add an output asset toocontain hello results of hello job. 
        task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.None);

        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
        job.Submit();
        job.GetExecutionProgressTask(CancellationToken.None).Wait();

        return job.OutputMediaAssets[0];
    }


> [!NOTE]
> Limitations actuelles :
>
> paramètre d’opacité superposition Hello n’est pas pris en charge.
>
> Votre fichier vidéo source et le fichier d’image de superposition hello ont toobe dans hello même actif et hello fichier vidéo besoins toobe ensemble en tant que fichier primaire de hello dans cet élément multimédia.
>
>

### <a name="json-preset"></a>Présélection JSON
    {
      "Version": 1.0,
      "Sources": [
        {
          "Streams": [],
          "Filters": {
            "VideoOverlay": {
              "Position": {
                "X": 100,
                "Y": 100,
                "Width": 100,
                "Height": 50
              },
              "AudioGainLevel": 0.0,
              "MediaParams": [
                {
                  "OverlayLoopCount": 1
                },
                {
                  "IsOverlay": true,
                  "OverlayLoopCount": 1,
                  "InputLoop": true
                }
              ],
              "Source": "Image001.png",
              "Clip": {
                "Duration": "00:00:05"
              },
              "FadeInDuration": {
                "Duration": "00:00:01"
              },
              "FadeOutDuration": {
                "StartTime": "00:00:03",
                "Duration": "00:00:04"
              }
            }
          },
          "Pad": true
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1045,
              "MaxBitrate": 1045,
              "BufferWindow": "00:00:05",
              "ReferenceFrames": 3,
              "EntropyMode": "Cavlc",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Type": "CopyAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}{Extension}",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <a name="xml-preset"></a>Présélection XML
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source>
          <Streams />
          <Filters>
            <VideoOverlay>
              <Source>Image001.png</Source>
              <Clip Duration="PT5S" />
              <FadeInDuration Duration="PT1S" />
              <FadeOutDuration StartTime="PT3S" Duration="PT4S" />
              <Position X="100" Y="100" Width="100" Height="50" />
              <Opacity>0</Opacity>
              <AudioGainLevel>0</AudioGainLevel>
              <MediaParams>
                <MediaParam>
                  <IsOverlay>false</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>false</InputLoop>
                </MediaParam>
                <MediaParam>
                  <IsOverlay>true</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>true</InputLoop>
                </MediaParam>
              </MediaParams>
            </VideoOverlay>
          </Filters>
          <Pad>true</Pad>
        </Source>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>1045</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>0</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cavlc</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1045</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <CopyAudio />
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}{Extension}">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>


## <a id="silent_audio"></a>Insertion d’une piste audio en mode silencieux lorsque l’entrée ne produit pas de son
Par défaut, si vous envoyez un encodeur toohello d’entrée qui contient uniquement, audio et vidéo aucun, hello élément multimédia de sortie contient des fichiers qui contiennent des données vidéo uniquement. Certains lecteurs ne pourront peut-être toohandle ce flux de sortie. Vous pouvez utiliser cette tooadd d’encodeur de paramètre tooforce hello une sortie toohello de piste audio en mode silencieux dans ce scénario.

tooforce hello encodeur tooproduce un élément multimédia contenant une piste audio en mode silencieux lors de l’entrée ne contient aucune donnée audio, spécifier la valeur de « InsertSilenceIfNoAudio » hello.

Vous pouvez effectuer les hello MES Présélections documentées dans [cela](media-services-mes-presets-overview.md) section et rendre hello après modification :

### <a name="json-preset"></a>Présélection JSON
    {
      "Channels": 2,
      "SamplingRate": 44100,
      "Bitrate": 96,
      "Type": "AACAudio",
      "Condition": "InsertSilenceIfNoAudio"
    }

### <a name="xml-preset"></a>Présélection XML
    <AACAudio Condition="InsertSilenceIfNoAudio">
      <Channels>2</Channels>
      <SamplingRate>44100</SamplingRate>
      <Bitrate>96</Bitrate>
    </AACAudio>

## <a id="deinterlacing"></a>Désactiver le désentrelacement automatique
Les clients ne doivent toodo rien si elles comme hello entrelacement toobe contenu automatiquement désactivé entrelacée. Lorsque hello automatique désentrelacement est sur hello (par défaut) MES hello détection d’images entrelacées automatique et uniquement, déduplication interlaces frames marqués comme entrelacé.

Vous pouvez désactiver automatiquement hello désentrelacement. Cette option n’est pas recommandée.

### <a name="json-preset"></a>Présélection JSON
    "Sources": [
    {
     "Filters": {
        "Deinterlace": {
          "Mode": "Off"
        }
      },
    }
    ]

### <a name="xml-preset"></a>Présélection XML
    <Sources>
    <Source>
      <Filters>
        <Deinterlace>
          <Mode>Off</Mode>
        </Deinterlace>
      </Filters>
    </Source>
    </Sources>


## <a id="audio_only"></a>Présélections audio uniquement
Cette section présente deux présélections MES audio uniquement : Audio AAC et Bonne qualité audio AAC.

### <a name="aac-audio"></a>Audio AAC
    {
      "Version": 1.0,
      "Codecs": [
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

### <a name="aac-good-quality-audio"></a>Bonne qualité audio AAC
    {
      "Version": 1.0,
      "Codecs": [
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 192,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <a id="concatenate"></a>Concaténation de deux fichiers vidéo ou plus

Hello exemple suivant illustre comment vous pouvez générer une présélection tooconcatenate deux ou plusieurs fichiers vidéos. scénario le plus courant Hello est lorsque vous souhaitez tooadd un en-tête ou une vidéo principale toohello de code de fin. Hello prévu est lorsque les fichiers vidéo hello en cours de modification ensemble partagent des propriétés (résolution, fréquence d’images, nombre de pistes audio, etc.). Vous devez prendre soin pas toomix vidéos de fréquences d’images différent ou avec le même nombre de pistes audio.

>[!NOTE]
>Hello conception actuelle de la fonctionnalité de concaténation hello attend que hello entrée clips vidéo sont cohérentes en termes de résolution, etc. fréquence d’images. 

### <a name="requirements-and-considerations"></a>Conditions requises et éléments à prendre en compte

* Les vidéos d'entrée ne doivent avoir qu'une seule piste audio.
* Entrée vidéos doivent tous avoir hello même fréquence d’images.
* Vous devez télécharger vos vidéos dans des éléments multimédias séparés et définir les vidéos hello comme fichier principal de hello dans chaque élément multimédia.
* Vous devez la durée de hello tooknow des vidéos.
* Hello prédéfinis exemples ci-dessous suppose que toutes les vidéos d’entrée hello démarrer avec un horodatage égal à zéro. Vous devez les valeurs StartTime toomodify hello si les vidéos hello ont cachet temporel de départ différentes, comme c’est généralement hello cas avec des archives en direct.
* Hello présélection JSON, les références explicites toohello AssetID valeurs d’éléments multimédias en entrée hello.
* exemple de code Hello suppose que hello que JSON prédéfini a été enregistré tooa fichier local, tel que « C:\supportFiles\preset.json ». Il suppose également que les deux composants ont été créés en téléchargeant des fichiers vidéos deux, et connaître les valeurs résultantes AssetID hello.
* Hello extrait de code et JSON présélection montre un exemple de la concaténation de deux fichiers vidéos. Vous pouvez l’étendre toomore que deux vidéos par :

  1. Tâche de l’appel. InputAssets.Add() à plusieurs reprises tooadd plus de vidéos, dans l’ordre.
  2. Rendre correspondant modifie élément toohello « Sources » Bonjour JSON, en ajoutant des entrées de plus, Bonjour même ordre.

### <a name="net-code"></a>Code .NET

    IAsset asset1 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:606db602-efd7-4436-97b4-c0b867ba195b").FirstOrDefault();
    IAsset asset2 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e").FirstOrDefault();

    // Declare a new job.
    IJob job = _context.Jobs.Create("Media Encoder Standard Job for Concatenating Videos");
    // Get a media processor reference, and pass tooit hello name of the
    // processor toouse for hello specific task.
    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

    // Load hello XML (or JSON) from hello local file.
    string configuration = File.ReadAllText(@"c:\supportFiles\preset.json");

    // Create a task
    ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
        processor,
        configuration,
        TaskOptions.None);

    // Specify hello input videos toobe concatenated (in order).
    task.InputAssets.Add(asset1);
    task.InputAssets.Add(asset2);
    // Add an output asset toocontain hello results of hello job.
    // This output is specified as AssetCreationOptions.None, which
    // means hello output asset is not encrypted.
    task.OutputAssets.AddNew("Output asset",
        AssetCreationOptions.None);

    job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
    job.Submit();
    job.GetExecutionProgressTask(CancellationToken.None).Wait();

### <a name="json-preset"></a>Présélection JSON

Mettre à jour votre paramètre prédéfini avec les ID des ressources hello que vous souhaitez tooconcatenate et avec le segment du moment opportun hello pour chaque vidéo.

    {
      "Version": 1.0,
      "Sources": [
        {
          "AssetID": "606db602-efd7-4436-97b4-c0b867ba195b",
          "StartTime": "00:00:01",
          "Duration": "00:00:15"
        },
        {
          "AssetID": "a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e",
          "StartTime": "00:00:02",
          "Duration": "00:00:05"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": true,
          "H264Layers": [
            {
              "Level": "auto",
              "Bitrate": 1800,
              "MaxBitrate": 1800,
              "BufferWindow": "00:00:05",
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <a id="crop"></a>Rogner des vidéos avec l’encodeur multimédia standard
Consultez hello [rogner vidéos avec Media Encoder Standard](media-services-crop-video.md) rubrique.

## <a id="no_video"></a>Insertion d’une piste vidéo lorsque l’entrée ne comporte aucune vidéo

Par défaut, si vous envoyez un encodeur toohello d’entrée qui contient uniquement des données audio et aucune vidéo, hello élément multimédia de sortie contient des fichiers qui contiennent des données audio uniquement. Certains lecteurs, y compris Azure Media Player (consultez [cela](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) ne peut pas être en mesure de toohandle ces flux de données. Vous pouvez utiliser cette tooadd d’encodeur paramètre tooforce hello une sortie de toohello monochrome piste vidéo dans ce scénario.

> [!NOTE]
> Forcer le hello encodeur tooinsert une piste vidéo sortie augmente la taille hello Hello Asset de sortie et hello ainsi les coûts pour hello tâche de codage. Vous devez exécuter des tests tooverify cette augmentation résultante a uniquement un faible impact sur votre facture mensuelle.
>

### <a name="inserting-video-at-only-hello-lowest-bitrate"></a>Insertion de vidéo avec uniquement le débit de la plus basse hello

Supposons que vous utilisez un encodage de vitesse de transmission plusieurs prédéfini tel que [« H264 plusieurs débits binaires 720p «](media-services-mes-preset-h264-multiple-bitrate-720p.md) tooencode l’intégralité de votre entrée de catalogue pour la diffusion en continu, qui contient un mélange de fichiers vidéos et audio uniquement. Dans ce scénario, lorsque hello entrée ne comporte aucune vidéo, vous souhaiterez tooforce hello encodeur tooinsert un monochrome vidéo suivre à simplement hello plus faible vitesse de transmission, sous la forme d’opposition tooinserting vidéo à chaque vitesse de transmission de sortie. tooachieve, vous devez toouse hello **InsertBlackIfNoVideoBottomLayerOnly** indicateur.

Vous pouvez effectuer les hello MES Présélections documentées dans [cela](media-services-mes-presets-overview.md) section et rendre hello après modification :

#### <a name="json-preset"></a>Présélection JSON
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideoBottomLayerOnly",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a>Présélection XML

Lors de l’utilisation de XML, utilisez la Condition = « InsertBlackIfNoVideoBottomLayerOnly » comme un attribut de toohello **H264Video** élément et la Condition = « InsertSilenceIfNoAudio » en tant qu’attribut trop**AACAudio**.

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideoBottomLayerOnly">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .
```

### <a name="inserting-video-at-all-output-bitrates"></a>Insertion de vidéo à tous les débits binaires de sortie
Supposons que vous utilisez un encodage de vitesse de transmission plusieurs prédéfini tel que [« H264 plusieurs débits binaires 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) tooencode l’intégralité de votre entrée de catalogue pour la diffusion en continu, qui contient un mélange de fichiers vidéos et audio uniquement. Dans ce scénario, lorsque hello entrée ne comporte aucune vidéo, vous souhaiterez tooforce hello encodeur tooinsert suivre d’une vidéo monochrome à tous les débits binaires de sortie hello. Cela garantit que votre sortie actifs sont tous homogènes avec toonumber en ce qui concerne des pistes vidéo et des pistes audio. tooachieve, vous devez toospecify hello indicateur de « InsertBlackIfNoVideo ».

Vous pouvez effectuer les hello MES Présélections documentées dans [cela](media-services-mes-presets-overview.md) section et rendre hello après modification :

#### <a name="json-preset"></a>Présélection JSON
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideo",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a>Présélection XML

Lors de l’utilisation de XML, utilisez la Condition = « InsertBlackIfNoVideo » comme un attribut de toohello **H264Video** élément et la Condition = « InsertSilenceIfNoAudio » en tant qu’attribut trop**AACAudio**.

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideo">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .  
```

## <a id="rotate_video"></a>Faire pivoter une vidéo
Hello [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) prend en charge de la rotation par les angles de 0/90/180/270. comportement par défaut de Hello est « Auto », où il tente de métadonnées de rotation toodetect hello dans le fichier vidéo entrant hello et compensation. Suivants de hello **Sources** tooone élément des présélections hello défini dans [cela](media-services-mes-presets-overview.md) section :

### <a name="json-preset"></a>Présélection JSON
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...
### <a name="xml-preset"></a>Présélection XML
    <Sources>
           <Source>
          <Streams />
          <Filters>
            <Rotation>90</Rotation>
          </Filters>
        </Source>
    </Sources>

Consultez également [cela](media-services-mes-schema.md#PreserveResolutionAfterRotation) rubrique pour plus d’informations sur comment encoder de hello interprète les paramètres de largeur et hauteur hello Bonjour prédéfini, lorsque la compensation de rotation est déclenchée.

Vous pouvez utiliser hello la valeur « 0 » tooindicate toohello encodeur tooignore rotation métadonnées, le cas échéant, dans la vidéo d’entrée de hello.

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Voir aussi
[Vue d’ensemble de l’encodage de Media Services](media-services-encode-asset.md)
