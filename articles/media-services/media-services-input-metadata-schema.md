---
title: "schéma de métadonnées d’entrée de Media Services aaaAzure | Documents Microsoft"
description: "rubrique de Hello donne une vue d’ensemble du schéma de métadonnées d’entrée Azure Media Services."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: d72848e2-4b65-4c84-94bc-e2a90a6e7f47
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 9b72c6ff317aa98451ea75548465dc6023b44a55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="input-metadata"></a>Métadonnées d'entrée
Un travail d’encodage est associé à un élément multimédia d’entrée (ou actifs) sur lequel vous souhaitez tooperform certaines tâches d’encodage.  À l’achèvement d’une tâche, une ressource de sortie est générée.  la ressource en sortie Hello contient vidéo, audio, des miniatures, manifestes, etc. hello ressource en sortie contient également un fichier contenant des métadonnées sur l’élément multimédia d’entrée de hello. nom du fichier XML de métadonnées hello Hello a hello suivant le format : &lt;id_élément_multimédia&gt;_metadata.xml (par exemple, 41114ad3-eb5e - 4c 57-8d92-5354e2b7d4a4_metadata), où &lt;id_ressource&gt; est hello AssetId valeur de l’élément multimédia d’entrée de hello.  

Si vous souhaitez que le fichier de métadonnées tooexamine hello, vous pouvez créer un **SAS** recherche et le téléchargement hello ordinateur local tooyour de fichier. Vous trouverez un exemple sur la façon de toocreate un localisateur SAS et télécharger un fichier [à l’aide des Extensions de hello Media Services .NET SDK](media-services-dotnet-get-started.md).  

Cette rubrique décrit les éléments de hello et types de schéma XML de hello de quels des métadonnées d’entrée de hello (&lt;id_élément_multimédia&gt;_metadata.xml) est basé.  Pour plus d’informations sur le fichier hello qui contient des métadonnées sur l’élément multimédia de sortie hello, consultez [sortie métadonnées](media-services-output-metadata-schema.md).  

> [!NOTE]
> Vous pouvez trouver hello [Code schéma](media-services-input-metadata-schema.md#code) un [exemple XML](media-services-input-metadata-schema.md#xml) à fin hello de cette rubrique.  
> 
> 

## <a name="AssetFiles"></a> Élément AssetFiles (élément racine)
Contient une collection de [élément AssetFile](media-services-input-metadata-schema.md#AssetFile)s pour le travail d’encodage hello.  

Voir un exemple XML à la fin de hello de cette rubrique : [exemple XML](media-services-input-metadata-schema.md#xml).  

| Nom | Description |
| --- | --- |
| **AssetFile**<br /><br /> minOccurs="1" maxOccurs="unbounded" |Un élément enfant unique. Pour plus d'informations, consultez la page [Élément AssetFile](media-services-input-metadata-schema.md#AssetFile). |

## <a name="AssetFile"></a> Élément AssetFile
 Contient des attributs et des éléments qui décrivent une ressource.  

 Voir un exemple XML à la fin de hello de cette rubrique : [exemple XML](media-services-input-metadata-schema.md#xml).  

### <a name="attributes"></a>Attributs
| Nom | Type | Description |
| --- | --- | --- |
| **Name**<br /><br /> Requis |**xs:string** |Nom du fichier de ressource. |
| **Taille**<br /><br /> Requis |**xs:long** |Taille de fichier d’élément multimédia hello en octets. |
| **Durée**<br /><br /> Requis |**xs:duration** |Durée de lecture du contenu. Exemple : Duration="PT25M37.757S". |
| **NumberOfStreams**<br /><br /> Requis |**xs:int** |Nombre de flux dans le fichier d’élément multimédia hello. |
| **FormatNames**<br /><br /> Requis |**xs:string** |Noms de format. |
| **FormatVerboseNames**<br /><br /> Requis |**xs:string** |Noms détaillés des formats. |
| **StartTime** |**xs:duration** |Heure de début du contenu. Exemple : StartTime="PT2.669S". |
| **OverallBitRate** |**xs:int** |Débit binaire moyen du fichier d’actif hello en Kbits/s. |

> [!NOTE]
> Hello les 4 éléments enfants doit apparaître dans une séquence.  
> 
> 

### <a name="child-elements"></a>Éléments enfants
| Nom | Type | Description |
| --- | --- | --- |
| **Programmes**<br /><br /> minOccurs="0" | |Collection de tous les [élément Programs](media-services-input-metadata-schema.md#Programs) lorsque le fichier d’élément multimédia hello est dans un format MPEG-TS. |
| **VideoTracks**<br /><br /> minOccurs="0" | |Chaque élément AssetFile physique peut contenir zéro ou plusieurs pistes vidéo entrelacées dans un format de conteneur approprié. Cet élément constituée une collection de tous les [élément VideoTracks](media-services-input-metadata-schema.md#VideoTracks) qui font partie d’un fichier d’élément multimédia hello. |
| **AudioTracks**<br /><br /> minOccurs="0" | |Chaque élément AssetFile physique peut contenir zéro ou plusieurs pistes audio entrelacées dans un format de conteneur approprié. Cet élément constituée une collection de tous les [élément AudioTracks](media-services-input-metadata-schema.md#AudioTracks) qui font partie d’un fichier d’élément multimédia hello. |
| **Métadonnées**<br /><br /> minOccurs="0" maxOccurs="unbounded" |[MetadataType](media-services-input-metadata-schema.md#MetadataType) |Les métadonnées du fichier de ressource représentées sous la forme de chaînes clé/valeur. Par exemple :<br /><br /> **&lt;Metadata key="language" value="eng" /&gt;** |

## <a name="TrackType"></a> TrackType
Voir un exemple XML à la fin de hello de cette rubrique : [exemple XML](media-services-input-metadata-schema.md#xml).  

### <a name="attributes"></a>Attributs
| Nom | Type | Description |
| --- | --- | --- |
| **Id**<br /><br /> Requis |**xs:int** |Index de base zéro de cette piste audio ou vidéo.<br /><br /> Cela n’est pas nécessairement que hello trackid tel qu’utilisé dans un fichier MP4. |
| **Codec** |**xs:string** |Chaîne de codec de la piste vidéo. |
| **CodecLongName** |**xs:string** |Nom long du codec de piste audio ou vidéo. |
| **TimeBase**<br /><br /> Requis |**xs:string** |Période. Exemple : TimeBase="1/48000" |
| **NumberOfFrames** |**xs:int** |Nombre de trames (présent pour les pistes vidéo). |
| **StartTime** |**xs:duration** |Suivre l’heure de début. Exemple : StartTime="PT2.669S" |
| **Durée** |**xs:duration** |Durée de la piste. Exemple : Duration="PTSampleFormat M37.757S". |

> [!NOTE]
> Hello les 2 éléments enfants doit apparaître dans une séquence.  
> 
> 

### <a name="child-elements"></a>Éléments enfants
| Nom | Type | Description |
| --- | --- | --- |
| **Disposition**<br /><br /> minOccurs="0" maxOccurs="1" |[StreamDispositionType](media-services-input-metadata-schema.md#StreamDispositionType) |Contient des informations de présentation (par exemple, si une piste audio particulière est destinée aux utilisateurs malvoyants). |
| **Métadonnées**<br /><br /> minOccurs="0" maxOccurs="unbounded" |[MetadataType](media-services-input-metadata-schema.md#MetadataType) |Chaînes clé/valeur générique qui peuvent être utilisé toohold diverses informations. Par exemple, key=”language”, et value=”eng”. |

## <a name="AudioTrackType"></a> AudioTrackType (hérite de TrackType)
 **AudioTrackType** est un type complexe global qui hérite de [TrackType](media-services-input-metadata-schema.md#TrackType).  

 type de Hello représente une piste audio spécifique dans le fichier d’élément multimédia hello.  

 Voir un exemple XML à la fin de hello de cette rubrique : [exemple XML](media-services-input-metadata-schema.md#xml).  

### <a name="attributes"></a>Attributs
| Nom | Type | Description |
| --- | --- | --- |
| **SampleFormat** |**xs:string** |Exemple de format. |
| **ChannelLayout** |**xs:string** |Disposition de canal. |
| **Canaux**<br /><br /> Requis |**xs:int** |Nombre (0 ou plus) de canaux audio. |
| **SamplingRate**<br /><br /> Requis |**xs:int** |Taux d’échantillonnage audio en échantillons/sec ou Hz. |
| **Bitrate** |**xs:int** |Débit binaire audio moyen en bits par seconde, tel que calculé à partir du fichier d’élément multimédia hello. Seulement charge utile hello flux élémentaire est comptée et surcharge de packaging hello n’est pas inclus dans ce nombre. |
| **BitsPerSample** |**xs:int** |Type de bits par échantillon pour le format wFormatTag hello. |

## <a name="VideoTrackType"></a> VideoTrackType (hérite de TrackType)
**VideoTrackType** est un type complexe global qui hérite de [TrackType](media-services-input-metadata-schema.md#TrackType).  

type de Hello représente une piste vidéo spécifique dans le fichier d’élément multimédia hello.  

Voir un exemple XML à la fin de hello de cette rubrique : [exemple XML](media-services-input-metadata-schema.md#xml).  

### <a name="attributes"></a>Attributs
| Nom | Type | Description |
| --- | --- | --- |
| **FourCC**<br /><br /> Requis |**xs:string** |Code FourCC du codec vidéo. |
| **Profil** |**xs:string** |Profil de la piste vidéo. |
| **Niveau** |**xs:string** |Niveau de la piste vidéo. |
| **PixelFormat** |**xs:string** |Format de pixel de la piste vidéo. |
| **Largeur**<br /><br /> Requis |**xs:int** |Largeur vidéo encodée en pixels. |
| **Hauteur**<br /><br /> Requis |**xs:int** |Hauteur vidéo encodée en pixels. |
| **DisplayAspectRatioNumerator**<br /><br /> Requis |**xs:double** |Numérateur des proportions d’affichage vidéo. |
| **DisplayAspectRatioDenominator**<br /><br /> Requis |**xs:double** |Dénominateur des proportions d’affichage vidéo. |
| **DisplayAspectRatioDenominator**<br /><br /> Requis |**xs:double** |Numérateur des proportions d’échantillon vidéo. |
| **SampleAspectRatioNumerator** |**xs:double** |Numérateur des proportions d’échantillon vidéo. |
| **SampleAspectRatioNumerator** |**xs:double** |Dénominateur des proportions d’échantillon vidéo. |
| **FrameRate**<br /><br /> Requis |**xs:decimal** |Fréquence d’images vidéo mesurée au format .3f. |
| **Bitrate** |**xs:int** |Débit binaire vidéo moyen en kilobits par seconde, tel que calculé à partir du fichier d’élément multimédia hello. Seulement charge utile hello flux élémentaire est comptée et surcharge de packaging hello n’est pas inclus. |
| **MaxGOPBitrate** |**xs:int** |Vitesse de transmission moyenne GOP maximum pour cette piste vidéo, en kilobits par seconde. |
| **HasBFrames** |**xs:int** |Numéro de piste vidéo des trames B. |

## <a name="MetadataType"></a> MetadataType
**MetadataType** est un type complexe global qui décrit les métadonnées d’un fichier de ressource en tant que chaînes clé/valeur. Par exemple, key=”language”, et value=”eng”.  

Voir un exemple XML à la fin de hello de cette rubrique : [exemple XML](media-services-input-metadata-schema.md#xml).  

### <a name="attributes"></a>Attributs
| Nom | Type | Description |
| --- | --- | --- |
| **key**<br /><br /> Requis |**xs:string** |clé Hello dans la paire clé/valeur de hello. |
| **value**<br /><br /> Requis |**xs:string** |valeur de Hello dans la paire clé/valeur de hello. |

## <a name="ProgramType"></a> ProgramType
**ProgramType** est un type complexe global qui décrit un programme.  

### <a name="attributes"></a>Attributs
| Nom | Type | Description |
| --- | --- | --- |
| **ProgramId**<br /><br /> Requis |**xs:int** |ID de programme |
| **NumberOfPrograms**<br /><br /> Requis |**xs:int** |Nombre de programmes. |
| **PmtPid**<br /><br /> Requis |**xs:int** |Les tables de correspondance de programme (PMT) contiennent des informations sur les programmes.  Pour plus d'informations, consultez [PMt](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT). |
| **PcrPid**<br /><br /> Requis |**xs:int** |Utilisé par le décodeur. Pour plus d'informations, consultez [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR) |
| **StartPTS** |**xs: long** |Horodatage de début de présentation. |
| **EndPTS** |**xs: long** |Horodatage de fin de présentation. |

## <a name="StreamDispositionType"></a> StreamDispositionType
**StreamDispositionType** est un type complexe global qui décrit le flux de données hello.  

Voir un exemple XML à la fin de hello de cette rubrique : [exemple XML](media-services-input-metadata-schema.md#xml).  

### <a name="attributes"></a>Attributs
| Nom | Type | Description |
| --- | --- | --- |
| **Par défaut**<br /><br /> Requis |**xs:int** |Définissez cette tooindicate de too1 attribut de qu'il s’agit présentation par défaut de hello. |
| **Dub**<br /><br /> Requis |**xs:int** |Définissez cette propriété cette tooindicate de too1 d’attribut est hello doublage de présentation. |
| **Ressource d’origine**<br /><br /> Requis |**xs:int** |Définition de cette tooindicate de too1 attribut de qu'il s’agit la présentation d’origine de hello. |
| **Commentaire**<br /><br /> Requis |**xs:int** |Définissez cette tooindicate de too1 attribut cette piste contient des commentaires. |
| **Lyrics**<br /><br /> Requis |**xs:int** |Définissez cette tooindicate de too1 attribut cette piste contient des paroles. |
| **Karaoke**<br /><br /> Requis |**xs:int** |Affectez cette tooindicate de too1 attribut représente hello piste karaoké (musique de fond, aucune voix). |
| **Forced**<br /><br /> Requis |**xs:int** |Définition de cette tooindicate de too1 attribut de qu'il s’agit la présentation de hello forcé. |
| **HearingImpaired**<br /><br /> Requis |**xs:int** |Définissez cette tooindicate de too1 attribut que cette piste est destinée aux personnes malentendantes de hello. |
| **VisualImpaired**<br /><br /> Requis |**xs:int** |Définissez cette tooindicate de too1 attribut que cette piste est destinée hello malvoyants. |
| **CleanEffects**<br /><br /> Requis |**xs:int** |Définissez cette tooindicate de too1 attribut que cette piste contient effets propres. |
| **AttachedPic**<br /><br /> Requis |**xs:int** |Définir ce tooindicate de too1 attribut que cette piste contient des images. |

## <a name="Programs"></a> Programmes (élément)
Élément wrapper contenant plusieurs éléments **Program**.  

### <a name="child-elements"></a>Éléments enfants
| Nom | Type | Description |
| --- | --- | --- |
| **Programme**<br /><br /> minOccurs="0" maxOccurs="unbounded" |[ProgramType](media-services-input-metadata-schema.md#ProgramType) |Pour les fichiers de ressources qui sont dans un format MPEG-TS, contient des informations sur les programmes dans le fichier d’élément multimédia hello. |

## <a name="VideoTracks"></a> Élément VideoTracks
 Élément wrapper contenant plusieurs éléments **VideoTrack**.  

 Voir un exemple XML à la fin de hello de cette rubrique : [exemple XML](media-services-input-metadata-schema.md#xml).  

### <a name="child-elements"></a>Éléments enfants
| Nom | Type | Description |
| --- | --- | --- |
| **VideoTrack**<br /><br /> minOccurs="0" maxOccurs="unbounded" |[VideoTrackType (hérite de TrackType)](media-services-input-metadata-schema.md#VideoTrackType) |Contient des informations sur les pistes vidéo dans le fichier d’élément multimédia hello. |

## <a name="AudioTracks"></a> Élément AudioTracks
 Élément wrapper contenant plusieurs éléments **AudioTrack**.  

 Voir un exemple XML à la fin de hello de cette rubrique : [exemple XML](media-services-input-metadata-schema.md#xml).  

### <a name="elements"></a>elements
| Nom | Type | Description |
| --- | --- | --- |
| **AudioTrack**<br /><br /> minOccurs="0" maxOccurs="unbounded" |[AudioTrackType (hérite de TrackType)](media-services-input-metadata-schema.md#AudioTrackType) |Contient des informations sur les pistes audio dans le fichier d’élément multimédia hello. |

## <a name="code"></a> Code du schéma
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" version="1.0"  
               xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               targetNamespace="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               elementFormDefault="qualified">  

      <xs:complexType name="MetadataType">  
        <xs:attribute name="key"   type="xs:string" use="required"/>  
        <xs:attribute name="value" type="xs:string" use="required"/>  
      </xs:complexType>  

      <xs:complexType name="ProgramType">  
        <xs:attribute name="ProgramId" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Program Id</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfPrograms" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Number of programs</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PmtPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pmt pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PcrPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pcr pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="StartPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>start pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="EndPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>end pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="StreamDispositionType">  
        <xs:attribute name="Default"          type="xs:int" use="required" />  
        <xs:attribute name="Dub"              type="xs:int" use="required" />  
        <xs:attribute name="Original"         type="xs:int" use="required" />  
        <xs:attribute name="Comment"          type="xs:int" use="required" />  
        <xs:attribute name="Lyrics"           type="xs:int" use="required" />  
        <xs:attribute name="Karaoke"          type="xs:int" use="required" />  
        <xs:attribute name="Forced"           type="xs:int" use="required" />  
        <xs:attribute name="HearingImpaired"  type="xs:int" use="required" />  
        <xs:attribute name="VisualImpaired"   type="xs:int" use="required" />  
        <xs:attribute name="CleanEffects"     type="xs:int" use="required" />  
        <xs:attribute name="AttachedPic"      type="xs:int" use="required" />  
      </xs:complexType>  

      <xs:complexType name="TrackType" abstract="true">  
        <xs:sequence>  
          <xs:element name="Disposition" type="StreamDispositionType" minOccurs="0" maxOccurs="1"/>  
          <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded"/>  
        </xs:sequence>  
        <xs:attribute name="Id" use="required">  
          <xs:annotation>  
            <xs:documentation>zero-based index of this video track. Note: this is not necessarily hello TrackID as used in an MP4 file</xs:documentation>  
          </xs:annotation>  
          <xs:simpleType>  
            <xs:restriction base="xs:int">  
              <xs:minInclusive value="0"/>  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:attribute>  
        <xs:attribute name="Codec" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec string</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="CodecLongName" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec long name</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="TimeBase"  type="xs:string" use="required">  
          <xs:annotation>  
            <xs:documentation>Time base. Example: TimeBase="1/48000"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfFrames">  
          <xs:annotation>  
            <xs:documentation>number of frames</xs:documentation>  
          </xs:annotation>  
          <xs:simpleType>  
            <xs:restriction base="xs:int">  
              <xs:minInclusive value="0"/>  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:attribute>  
        <xs:attribute name="StartTime" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track start time. Example: StartTime="PT2.669S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="Duration" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track duration. Example: Duration="PT25M37.757S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="VideoTrackType">  
        <xs:annotation>  
          <xs:documentation>A specific video track in hello parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="FourCC" type="xs:string" use="required">  
              <xs:annotation>  
                <xs:documentation>video codec FourCC code</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Profile" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>profile</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Level" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>level</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="PixelFormat" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>Video track's pixel format</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Width" use="required">  
              <xs:annotation>  
                <xs:documentation>encoded video width in pixels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Height" use="required">  
              <xs:annotation>  
                <xs:documentation>encoded video height in pixels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="DisplayAspectRatioNumerator" use="required">  
              <xs:annotation>  
                <xs:documentation>video display aspect ratio numerator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="DisplayAspectRatioDenominator" use="required">  
              <xs:annotation>  
                <xs:documentation>video display aspect ratio denominator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SampleAspectRatioNumerator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio numerator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SampleAspectRatioDenominator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio denominator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="FrameRate" use="required">  
              <xs:annotation>  
                <xs:documentation>measured video frame rate in .3f format</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:decimal">  
                  <xs:minInclusive value="0"/>  
                  <xs:fractionDigits value="3"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average video bit rate in kilobits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="MaxGOPBitrate">  
              <xs:annotation>  
                <xs:documentation>Max GOP average bitrate for this video track, in kilobits per second</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="HasBFrames" type="xs:int">  
              <xs:annotation>  
                <xs:documentation>video track number of B frames</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

      <xs:complexType name="AudioTrackType">  
        <xs:annotation>  
          <xs:documentation>a specific audio track in hello parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="SampleFormat"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>sample format</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="ChannelLayout"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>channel layout</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Channels" use="required">  
              <xs:annotation>  
                <xs:documentation>number of audio channels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SamplingRate" use="required">  
              <xs:annotation>  
                <xs:documentation>audio sampling rate in samples/sec or Hz</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average audio bit rate in bits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="BitsPerSample">  
              <xs:annotation>  
                <xs:documentation>Bits per sample for hello wFormatTag format type</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

      <xs:element name="AssetFiles">  
        <xs:annotation>  
          <xs:documentation>Collection of AssetFile entries for hello encoding job</xs:documentation>  
        </xs:annotation>  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="AssetFile" minOccurs="1" maxOccurs="unbounded">  
              <xs:annotation>  
                <xs:documentation>asset file</xs:documentation>  
              </xs:annotation>  
              <xs:complexType>  
                <xs:sequence>  
                  <xs:element name="Programs" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>This is hello collection of all programs when file is MPEG-TS</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Program" type="ProgramType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="VideoTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is hello collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" type="VideoTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="AudioTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is hello collection of all those audio tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="AudioTrack" type="AudioTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded" />  
                </xs:sequence>  
                <xs:attribute name="Name" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>hello media asset file name</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="Size" use="required">  
                  <xs:annotation>  
                    <xs:documentation>size of file in bytes</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:long">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
                <xs:attribute name="Duration" type="xs:duration" use="required">  
                  <xs:annotation>  
                    <xs:documentation>content play back duration. Example: Duration="PT25M37.757S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="NumberOfStreams" type="xs:int" use="required">  
                  <xs:annotation>  
                    <xs:documentation>number of streams in asset file</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatNames" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatVerboseName" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format verbose names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="StartTime" type="xs:duration">  
                  <xs:annotation>  
                    <xs:documentation>content start time. Example: StartTime="PT2.669S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="OverallBitRate">  
                  <xs:annotation>  
                    <xs:documentation>average bitrate of hello asset file in kbps</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:int">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:schema>  


## <a name="xml"></a> Exemple XML
Hello Voici un exemple de fichier de métadonnées d’entrée hello.  

    <?xml version="1.0" encoding="utf-8"?>  
    <AssetFiles xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata">  
      <AssetFile Name="bear.mp4" Size="1973733" Duration="PT12.678S" NumberOfStreams="2" FormatNames="mov,mp4,m4a,3gp,3g2,mj2" FormatVerboseName="QuickTime / MOV" StartTime="PT0S" OverallBitRate="1245">  
        <VideoTracks>  
          <VideoTrack Id="1" Codec="h264" CodecLongName="H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10" TimeBase="1/29970" NumberOfFrames="375" StartTime="PT0.034S" Duration="PT12.645S" FourCC="avc1" Profile="High" Level="4.1" PixelFormat="yuv420p" Width="512" Height="384" DisplayAspectRatioNumerator="4" DisplayAspectRatioDenominator="3" SampleAspectRatioNumerator="1" SampleAspectRatioDenominator="1" FrameRate="29.656" Bitrate="1043" HasBFrames="1">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Video Media Handler" />  
          </VideoTrack>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="aac" CodecLongName="AAC (Advanced Audio Coding)" TimeBase="1/44100" NumberOfFrames="546" StartTime="PT0S" Duration="PT12.678S" SampleFormat="fltp" ChannelLayout="stereo" Channels="2" SamplingRate="44100" Bitrate="156" BitsPerSample="0">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Sound Media Handler" />  
          </AudioTrack>  
        </AudioTracks>  
        <Metadata key="major_brand" value="mp42" />  
        <Metadata key="minor_version" value="0" />  
        <Metadata key="compatible_brands" value="mp42mp41" />  
        <Metadata key="creation_time" value="2010-03-10 16:11:53" />  
        <Metadata key="comment" value="Courtesy of National Geographic.  Used by Permission." />  
      </AssetFile>  
    </AssetFiles>  

## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

