---
title: "aaaHow toouse Blitline pour le traitement d’image - guide des fonctionnalités Azure"
description: "Découvrez comment toouse hello Blitline service tooprocess des images au sein d’une application Windows Azure."
services: 
documentationcenter: .net
author: blitline-dev
manager: jason@blitline.com
editor: jason@blitline.com
ms.assetid: 6c711248-0e52-4895-ba9e-8395628de924
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2014
ms.author: support@blitline.com
ms.openlocfilehash: 328fd177e25f45f29f8ad8e142d02b46017a858e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blitline-with-azure-and-azure-storage"></a>Comment toouse Blitline avec Azure et de stockage Azure
Ce guide explique comment tooaccess Blitline services et comment toosubmit travaux tooBlitline.

## <a name="what-is-blitline"></a>Présentation de Blitline
Blitline est une image basée sur le cloud service qui fournit le traitement d’image de niveau entreprise à une fraction de prix hello que coût toobuild de traitement il vous-même.

les faits Hello sont que le traitement d’image a été effectué indéfiniment, généralement reconstruits sol hello pour chaque site Web. Nous sommes bien placés pour le savoir, car nous en avons conçu un nombre incalculable de fois. Un jour, nous avons décidé qu'il était temps de proposer ce service à tout un chacun. Nous savons comment toodo il, toodo il rapidement et efficacement et enregistrer tout le monde fonctionnent dans hello entre-temps.

Pour plus d'informations, consultez la page [http://www.blitline.com](http://www.blitline.com).

## <a name="what-blitline-is-not"></a>Éléments non proposés par Blitline
tooclarify que Blitline est utile pour, il est souvent plus facile tooidentify que Blitline ne pas faire avant de le déplacer vers l’avant.

* Blitline n’a pas d’images de tooupload widgets HTML. Vous devez disposer des images disponibles publiquement ou avec des autorisations restreintes pour Blitline tooreach.
* Blitline n'offre pas de traitement d'image en direct, contrairement à Aviary.com.
* Blitline n’accepte pas de téléchargement des images, vous ne pouvez pas envoyer directement votre tooBlitline d’images. Vous devez les transmettre tooAzure stockage ou autres emplacements que blitline prend en charge et alors indiquer au Blitline où toogo les obtenir.
* Blitline est massivement parallèle et n'effectue pas de traitement synchrone. Vous devez nous fournir une URL de retour et nous vous préviendrons lorsque nous aurons fini le traitement.

## <a name="create-a-blitline-account"></a>Création d'un compte Blitline
[!INCLUDE [blitline-signup](../includes/blitline-signup.md)]

## <a name="how-toocreate-a-blitline-job"></a>Comment toocreate un travail Blitline
Blitline utilise JSON toodefine hello opérations tootake sur une image. Ce JSON se compose de quelques champs simples.

exemple Hello le plus simple est la suivante :

        json : '{
       "application_id": "MY_APP_ID",
       "src" : "http://cdn.blitline.com/filters/boys.jpeg",
       "functions" : [ {
           "name": "resize_to_fit",
           "params" : { "width": 240, "height": 140 },
           "save" : { "image_identifier" : "external_sample_1" }
       } ]
    }'

Ici, nous avons JSON qui effectuera une image « src » «... boys.jpeg » et que vous redimensionnez too240x140 de cette image.

Hello ID d’Application est un élément que vous pouvez trouver dans votre **informations de connexion** ou **gérer** onglet sur Azure. Il s’agit de votre identifiant secret qui vous permet des travaux toorun sur Blitline.

Hello « Enregistrer » paramètre identifie les informations où vous souhaitez que tooput hello image une fois que nous avons le traitement. Dans cet exemple sans importance, nous n'avons pas défini d'endroit. Si aucun endroit n'est défini, Blitline la stockera localement (et temporairement) dans un emplacement de cloud unique. Vous serez en mesure de tooget qui emplacement à partir de hello JSON retourné par Blitline lorsque vous apportez hello Blitline. identificateur de le « image » Hello est requis et est retourné tooyou lorsque tooidentify donnée enregistrée image.

Vous trouverez plus d’informations sur hello *fonctions* nous prenons en charge ici : <http://www.blitline.com/docs/functions>

Vous pouvez également rechercher la documentation sur hello ici les options de tâche : <http://www.blitline.com/docs/api>

Une fois que vous avez votre JSON vous toodo suffit **POST** il trop`http://api.blitline.com/job`

Le JSON renvoyé ressemblera à ceci :

    {
     "results":
         {"images":
            [{
              "image_identifier":"external_sample_1",
              "s3_url":"https://s3.amazonaws.com/dev.blitline/2011110722/YOUR_APP_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg"
            }],
          "job_id":"4eb8c9f72a50ee2a9900002f"
         }
    }


Vous pouvez en déduire que Blitline a reçu votre demande et il a le placer dans une file d’attente de traitement, et lorsqu’il se termine hello sera disponible à : **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_application\_ID /CK3f0xBF_2bV6wf7gEZE8w.jpg**

## <a name="how-toosave-an-image-tooyour-azure-storage-account"></a>Comment toosave un tooyour image du compte de stockage Azure
Si vous avez un compte de stockage Azure, vous pouvez facilement avoir Blitline les images de hello traitée par émission de données dans votre conteneur Azure. En ajoutant un « azure_destination », vous définissez les emplacement hello et les autorisations de toopush Blitline à.

Voici un exemple :

    job : '{
      "application_id": "YOUR_APP_ID",
      "src" : "http://www.google.com/logos/2011/houdini11-hp.jpg",
         "functions" : [{
         "name": "blur",
         "save" : {
             "image_identifier" : "YOUR_IMAGE_IDENTIFIER",
             "azure_destination" : {
                 "account_name" : "YOUR_AZURE_CONTAINER_NAME",
                 "shared_access_signature" : "SAS_THAT_GIVES_BLITLINE_PERMISSION_TO_WRITE_THIS_OBJECT_TO_CONTAINER",
               }
           }
         }]
       }'


En renseignant les valeurs hello CAPITALIZED avec votre propre, vous pouvez soumettre cette toohttp://api.blitline.com/job JSON et hello « src » image sera traitée avec un filtre Flou et puis envoyées tooyou destination Azure.

### <a name="please-note"></a>Notez ce qui suit :
Hello SAS doit contenir l’url SAS entière hello, y compris hello de nom de fichier du fichier de destination hello.

Exemple :

    http://blitline.blob.core.windows.net/sample/image.jpg?sr=b&sv=2012-02-12&st=2013-04-12T03%3A18%3A30Z&se=2013-04-12T04%3A18%3A30Z&sp=w&sig=Bte2hkkbwTT2sqlkkKLop2asByrE0sIfeesOwj7jNA5o%3D


Vous pouvez également lire hello dernière édition de documents de stockage Azure de Blitline [ici](http://www.blitline.com/docs/azure_storage).

## <a name="next-steps"></a>Étapes suivantes
Visitez tooread blitline.com sur nos autres fonctionnalités :

* Documents de point de terminaison d'API Blitline <http://www.blitline.com/docs/api>
* Fonctions d'API Blitline <http://www.blitline.com/docs/functions>
* Exemples d'API Blitline <http://www.blitline.com/docs/examples>
* Bibliothèque Nuget tierce <http://nuget.org/packages/Blitline.Net>

