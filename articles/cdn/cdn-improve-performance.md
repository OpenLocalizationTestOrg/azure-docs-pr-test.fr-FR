---
title: performances aaaImprove en compressant les fichiers dans le CDN Azure | Documents Microsoft
description: "Découvrez comment tooimprove fichier transférer les performances de chargement de page vitesse et augmentent par la compression des fichiers dans le CDN Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: af1cddff-78d8-476b-a9d0-8c2164e4de5d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 9a1698b6c29233c2e2e6fb17cdd8e919ae8bfa1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="improve-performance-by-compressing-files-in-azure-cdn"></a>Compression des fichiers dans Azure CDN pour améliorer les performances
La compression est une vitesse de transfert de fichier tooimprove méthode simple et efficace et performances de chargement de page augmentation en réduisant la taille du fichier avant qu’il sont envoyé à partir du serveur de hello. Elle permet de réduire les coûts de bande passante et offre à vos utilisateurs davantage de réactivité.

Il existe deux façons de tooenable compression :

* Vous pouvez activer la compression sur votre serveur d’origine, auquel cas hello CDN traverse hello des fichiers compressés et remettre les fichiers compressés tooclients qui les demandent.
* Vous pouvez activer la compression directement sur les serveurs de bord CDN, dans lequel cas hello CDN compresse hello des fichiers et servir les utilisateurs tooend, même si elles ne sont pas compressées par le serveur d’origine hello.

> [!IMPORTANT]
> Modifications de configuration CDN prendront certaines toopropagate de temps via le réseau de hello.  Pour les profils du <b>CDN Azure fourni par Akamai</b> , la propagation s’effectue généralement en moins d’une minute.  Pour les profils du <b>CDN Azure fourni par Verizon</b> , vous verrez généralement vos changements s’appliquer dans un délai de 90 minutes.  S’il s’agit hello première fois que vous avez configuré la compression pour votre point de terminaison CDN, vous devez envisager d’attente toobe 1 et 2 heures que la propagation des paramètres de compression de hello POP toohello avant la résolution des problèmes
> 
> 

## <a name="enabling-compression"></a>Activation de la compression
> [!NOTE]
> fournissent Hello niveaux Standard et Premium CDN hello les mêmes fonctionnalités de compression, mais diffère hello interface utilisateur.  Pour plus d’informations sur les différences de hello entre les niveaux Standard et Premium CDN, consultez [vue d’ensemble du CDN Azure](cdn-overview.md).
> 
> 

### <a name="standard-tier"></a>Niveau standard
> [!NOTE]
> Cette section s’applique également**Azure CDN Standard de Verizon** et **Azure CDN Standard à partir d’Akamai** profils.
> 
> 

1. À partir de la page de profil CDN hello, cliquez sur le point de terminaison CDN hello toomanage vous le souhaitez.
   
    ![Points de terminaison de la page de profil CDN](./media/cdn-file-compression/cdn-endpoints.png)
   
    page de point de terminaison CDN Hello s’ouvre.
2. Cliquez sur hello **configurer** bouton.
   
    ![Bouton de gestion de la page de profil CDN](./media/cdn-file-compression/cdn-config-btn.png)
   
    page de Configuration CDN Hello s’ouvre.
3. Activez **Compression**.
   
    ![Options de compression CDN](./media/cdn-file-compression/cdn-compress-standard.png)
4. Utiliser des types de valeur par défaut de hello, ou modifier la liste de hello en supprimant ou en ajoutant des types de fichiers.
   
   > [!TIP]
   > Tant que possible, il n’est pas recommandé tooapply compression toocompressed formats, tels que ZIP, MP3, MP4, JPG, etc..
   > 
   > 
5. Après avoir apporté vos modifications, cliquez sur hello **enregistrer** bouton.

### <a name="premium-tier"></a>Niveau Premium
> [!NOTE]
> Cette section s’applique également**Azure CDN Premium de Verizon** profils.
> 
> 

1. À partir de la page de profil hello CDN, cliquez sur hello **gérer** bouton.
   
    ![Bouton de gestion de la page de profil CDN](./media/cdn-file-compression/cdn-manage-btn.png)
   
    portail de gestion CDN Hello s’ouvre.
2. Pointage hello **grand HTTP** tab, puis pointez sur hello **paramètres de Cache** menu volant.  Cliquez sur **Compression**.

    ![Sélection de la compression de fichiers](./media/cdn-file-compression/cdn-compress-select.png)
   
    Les options de compression sont affichées.
   
    ![Compression de fichiers](./media/cdn-file-compression/cdn-compress-files.png)
3. Activer la compression en cliquant sur hello **Compression activée** case d’option.  Entrez les types MIME hello vous souhaitez toocompress sous la forme d’une liste délimitée par des virgules (sans espaces) Bonjour **Types de fichiers** zone de texte.
   
   > [!TIP]
   > Tant que possible, il n’est pas recommandé tooapply compression toocompressed formats, tels que ZIP, MP3, MP4, JPG, etc.. 
   > 
   > 
4. Après avoir apporté vos modifications, cliquez sur hello **mise à jour** bouton.

## <a name="compression-rules"></a>Règles de compression
Ces tableaux décrivent le comportement de compression du CDN Azure pour chaque scénario.

> [!IMPORTANT]
> Pour le **CDN Azure fourni par Verizon** (Standard et Premium), seuls les fichiers éligibles sont compressés.  un fichier de toobe éligible pour la compression, procédez comme suit :
> 
> * Être supérieur à 128 octets.
> * Être inférieur à 1 Mo.
> 
> Pour le **CDN Azure fourni par Akamai**, tous les fichiers sont éligibles à la compression.
> 
> Pour tous les produits Azure CDN, un fichier doit être de type MIME qui a été [configuré pour la compression](#enabling-compression).
> 
> Les profils **Azure CDN fourni par Verizon** (Standard et Premium) prennent en charge l’encodage **gzip** (zip GNU), **deflate**, **bzip2** ou **br** (Brotli). Pour l’encodage de Brotli, la compression de hello est effectuée uniquement sur le bord de hello. Hello client/navigateur doit envoyer la demande hello pour l’encodage de Brotli et asset compressé de hello doit avoir été compressé côté hello d’origine tout d’abord. 
>
>Les profils du **CDN Azure fourni par Akamai** prennent uniquement en charge l’encodage **gzip**.
> 
> **CDN Azure à partir d’Akamai** demande toujours des points de terminaison **gzip** de fichiers à partir de l’origine de hello, quelle que soit la demande du client hello codés. 

### <a name="compression-disabled-or-file-is-ineligible-for-compression"></a>Compression désactivée ou le fichier n’est pas éligible pour la compression
| Format demandé par le client (via l’en-tête Accept-Encoding) | Format de fichier mis en cache | Client de toohello réponse CDN | Remarques |
| --- | --- | --- | --- |
| Compressé |Compressé |Compressé | |
| Compressé |Non compressé |Non compressé | |
| Compressé |Non mis en cache |Compressés ou non compressé |Dépend de la réponse d’origine |
| Non compressé |Compressé |Non compressé | |
| Non compressé |Non compressé |Non compressé | |
| Non compressé |Non mis en cache |Non compressé | |

### <a name="compression-enabled-and-file-is-eligible-for-compression"></a>La compression est activée et le fichier est éligible pour la compression
| Format demandé par le client (via l’en-tête Accept-Encoding) | Format de fichier mis en cache | Client de toohello réponse CDN | Remarques |
| --- | --- | --- | --- |
| Compressé |Compressé |Compressé |Transcode CDN entre les formats pris en charge |
| Compressé |Non compressé |Compressé |CDN effectue la compression |
| Compressé |Non mis en cache |Compressé |CDN effectue la compression si l’origine renvoie le format non compressé.  **Azure CDN de Verizon** passe hello fichier non compressé sur la première demande de hello et puis compresse et caches hello fichier pour les demandes suivantes.  Les fichiers avec l’en-tête `Cache-Control: no-cache` ne seront jamais compressés. |
| Non compressé |Compressé |Non compressé |CDN effectue la décompression |
| Non compressé |Non compressé |Non compressé | |
| Non compressé |Non mis en cache |Non compressé | |

## <a name="media-services-cdn-compression"></a>Compression CDN Media Services
Media Services CDN activé des points de terminaison de diffusion en continu, la compression est activée par défaut pour les types de contenu suivants de hello : application/vnd.ms-sstr + xml, application/dash+xml,application/vnd.apple.mpegurl, application/f4m + xml. Vous ne pouvez pas activer/désactiver la compression pour hello mentionné types à l’aide de hello portail Azure.  

## <a name="see-also"></a>Voir aussi
* [Résolution des problèmes de compression des fichiers CDN](cdn-troubleshoot-compression.md)    

