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
# <a name="how-toouse-blitline-with-azure-and-azure-storage"></a><span data-ttu-id="8da44-103">Comment toouse Blitline avec Azure et de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="8da44-103">How toouse Blitline with Azure and Azure Storage</span></span>
<span data-ttu-id="8da44-104">Ce guide explique comment tooaccess Blitline services et comment toosubmit travaux tooBlitline.</span><span class="sxs-lookup"><span data-stu-id="8da44-104">This guide will explain how tooaccess Blitline services and how toosubmit jobs tooBlitline.</span></span>

## <a name="what-is-blitline"></a><span data-ttu-id="8da44-105">Présentation de Blitline</span><span class="sxs-lookup"><span data-stu-id="8da44-105">What is Blitline?</span></span>
<span data-ttu-id="8da44-106">Blitline est une image basée sur le cloud service qui fournit le traitement d’image de niveau entreprise à une fraction de prix hello que coût toobuild de traitement il vous-même.</span><span class="sxs-lookup"><span data-stu-id="8da44-106">Blitline is a cloud-based image processing service that provides enterprise level image processing at a fraction of hello price that it would cost toobuild it yourself.</span></span>

<span data-ttu-id="8da44-107">les faits Hello sont que le traitement d’image a été effectué indéfiniment, généralement reconstruits sol hello pour chaque site Web.</span><span class="sxs-lookup"><span data-stu-id="8da44-107">hello fact is that image processing has been done over and over again, usually rebuilt from hello ground up for each and every website.</span></span> <span data-ttu-id="8da44-108">Nous sommes bien placés pour le savoir, car nous en avons conçu un nombre incalculable de fois.</span><span class="sxs-lookup"><span data-stu-id="8da44-108">We realize this because we’ve built them a million times too.</span></span> <span data-ttu-id="8da44-109">Un jour, nous avons décidé qu'il était temps de proposer ce service à tout un chacun.</span><span class="sxs-lookup"><span data-stu-id="8da44-109">One day we decided that perhaps it‘s time we just do it for everyone.</span></span> <span data-ttu-id="8da44-110">Nous savons comment toodo il, toodo il rapidement et efficacement et enregistrer tout le monde fonctionnent dans hello entre-temps.</span><span class="sxs-lookup"><span data-stu-id="8da44-110">We know how toodo it, toodo it fast and efficiently, and save everyone work in hello meantime.</span></span>

<span data-ttu-id="8da44-111">Pour plus d'informations, consultez la page [http://www.blitline.com](http://www.blitline.com).</span><span class="sxs-lookup"><span data-stu-id="8da44-111">For more information, see [http://www.blitline.com](http://www.blitline.com).</span></span>

## <a name="what-blitline-is-not"></a><span data-ttu-id="8da44-112">Éléments non proposés par Blitline</span><span class="sxs-lookup"><span data-stu-id="8da44-112">What Blitline is NOT...</span></span>
<span data-ttu-id="8da44-113">tooclarify que Blitline est utile pour, il est souvent plus facile tooidentify que Blitline ne pas faire avant de le déplacer vers l’avant.</span><span class="sxs-lookup"><span data-stu-id="8da44-113">tooclarify what Blitline is useful for, it is often easier tooidentify what Blitline does NOT do before moving forward.</span></span>

* <span data-ttu-id="8da44-114">Blitline n’a pas d’images de tooupload widgets HTML.</span><span class="sxs-lookup"><span data-stu-id="8da44-114">Blitline does NOT have HTML widgets tooupload images.</span></span> <span data-ttu-id="8da44-115">Vous devez disposer des images disponibles publiquement ou avec des autorisations restreintes pour Blitline tooreach.</span><span class="sxs-lookup"><span data-stu-id="8da44-115">You must have images available publicly or with restricted permissions available for Blitline tooreach.</span></span>
* <span data-ttu-id="8da44-116">Blitline n'offre pas de traitement d'image en direct, contrairement à Aviary.com.</span><span class="sxs-lookup"><span data-stu-id="8da44-116">Blitline does NOT do live image processing, like Aviary.com</span></span>
* <span data-ttu-id="8da44-117">Blitline n’accepte pas de téléchargement des images, vous ne pouvez pas envoyer directement votre tooBlitline d’images.</span><span class="sxs-lookup"><span data-stu-id="8da44-117">Blitline does NOT accept image uploads, you cannot push your images tooBlitline directly.</span></span> <span data-ttu-id="8da44-118">Vous devez les transmettre tooAzure stockage ou autres emplacements que blitline prend en charge et alors indiquer au Blitline où toogo les obtenir.</span><span class="sxs-lookup"><span data-stu-id="8da44-118">You must push them tooAzure Storage or other places Blitline supports and then tell Blitline where toogo get them.</span></span>
* <span data-ttu-id="8da44-119">Blitline est massivement parallèle et n'effectue pas de traitement synchrone.</span><span class="sxs-lookup"><span data-stu-id="8da44-119">Blitline is massively parallel and does NOT do any synchronous processing.</span></span> <span data-ttu-id="8da44-120">Vous devez nous fournir une URL de retour et nous vous préviendrons lorsque nous aurons fini le traitement.</span><span class="sxs-lookup"><span data-stu-id="8da44-120">Meaning you must give us a postback_url and we can tell you when we are done processing.</span></span>

## <a name="create-a-blitline-account"></a><span data-ttu-id="8da44-121">Création d'un compte Blitline</span><span class="sxs-lookup"><span data-stu-id="8da44-121">Create a Blitline account</span></span>
[!INCLUDE [blitline-signup](../includes/blitline-signup.md)]

## <a name="how-toocreate-a-blitline-job"></a><span data-ttu-id="8da44-122">Comment toocreate un travail Blitline</span><span class="sxs-lookup"><span data-stu-id="8da44-122">How toocreate a Blitline job</span></span>
<span data-ttu-id="8da44-123">Blitline utilise JSON toodefine hello opérations tootake sur une image.</span><span class="sxs-lookup"><span data-stu-id="8da44-123">Blitline uses JSON toodefine hello actions you want tootake on an image.</span></span> <span data-ttu-id="8da44-124">Ce JSON se compose de quelques champs simples.</span><span class="sxs-lookup"><span data-stu-id="8da44-124">This JSON is composed of a few simple fields.</span></span>

<span data-ttu-id="8da44-125">exemple Hello le plus simple est la suivante :</span><span class="sxs-lookup"><span data-stu-id="8da44-125">hello simplest example is as follows:</span></span>

        json : '{
       "application_id": "MY_APP_ID",
       "src" : "http://cdn.blitline.com/filters/boys.jpeg",
       "functions" : [ {
           "name": "resize_to_fit",
           "params" : { "width": 240, "height": 140 },
           "save" : { "image_identifier" : "external_sample_1" }
       } ]
    }'

<span data-ttu-id="8da44-126">Ici, nous avons JSON qui effectuera une image « src » «... boys.jpeg » et que vous redimensionnez too240x140 de cette image.</span><span class="sxs-lookup"><span data-stu-id="8da44-126">Here we have JSON that will take a "src" image "...boys.jpeg" and then resize that image too240x140.</span></span>

<span data-ttu-id="8da44-127">Hello ID d’Application est un élément que vous pouvez trouver dans votre **informations de connexion** ou **gérer** onglet sur Azure.</span><span class="sxs-lookup"><span data-stu-id="8da44-127">hello Application ID is something you can find in your **CONNECTION INFO** or **MANAGE** tab on Azure.</span></span> <span data-ttu-id="8da44-128">Il s’agit de votre identifiant secret qui vous permet des travaux toorun sur Blitline.</span><span class="sxs-lookup"><span data-stu-id="8da44-128">It is your secret identifier that allows you toorun jobs on Blitline.</span></span>

<span data-ttu-id="8da44-129">Hello « Enregistrer » paramètre identifie les informations où vous souhaitez que tooput hello image une fois que nous avons le traitement.</span><span class="sxs-lookup"><span data-stu-id="8da44-129">hello "save" parameter identifies information about where you want tooput hello image once we have processed it.</span></span> <span data-ttu-id="8da44-130">Dans cet exemple sans importance, nous n'avons pas défini d'endroit.</span><span class="sxs-lookup"><span data-stu-id="8da44-130">In this trivial case, we haven't defined one.</span></span> <span data-ttu-id="8da44-131">Si aucun endroit n'est défini, Blitline la stockera localement (et temporairement) dans un emplacement de cloud unique.</span><span class="sxs-lookup"><span data-stu-id="8da44-131">If no location is defined Blitline will store it locally (and temporarily) at a unique cloud location.</span></span> <span data-ttu-id="8da44-132">Vous serez en mesure de tooget qui emplacement à partir de hello JSON retourné par Blitline lorsque vous apportez hello Blitline.</span><span class="sxs-lookup"><span data-stu-id="8da44-132">You will be able tooget that location from hello JSON returned by Blitline when you make hello Blitline.</span></span> <span data-ttu-id="8da44-133">identificateur de le « image » Hello est requis et est retourné tooyou lorsque tooidentify donnée enregistrée image.</span><span class="sxs-lookup"><span data-stu-id="8da44-133">hello "image" identifier is required and is returned tooyou when tooidentify this particular saved image.</span></span>

<span data-ttu-id="8da44-134">Vous trouverez plus d’informations sur hello *fonctions* nous prenons en charge ici : <http://www.blitline.com/docs/functions></span><span class="sxs-lookup"><span data-stu-id="8da44-134">You can find more information about hello *functions* we support here: <http://www.blitline.com/docs/functions></span></span>

<span data-ttu-id="8da44-135">Vous pouvez également rechercher la documentation sur hello ici les options de tâche : <http://www.blitline.com/docs/api></span><span class="sxs-lookup"><span data-stu-id="8da44-135">You can also find documentation about hello job options here: <http://www.blitline.com/docs/api></span></span>

<span data-ttu-id="8da44-136">Une fois que vous avez votre JSON vous toodo suffit **POST** il trop`http://api.blitline.com/job`</span><span class="sxs-lookup"><span data-stu-id="8da44-136">Once you have your JSON all you need toodo is **POST** it too`http://api.blitline.com/job`</span></span>

<span data-ttu-id="8da44-137">Le JSON renvoyé ressemblera à ceci :</span><span class="sxs-lookup"><span data-stu-id="8da44-137">You will get JSON back that looks something like this:</span></span>

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


<span data-ttu-id="8da44-138">Vous pouvez en déduire que Blitline a reçu votre demande et il a le placer dans une file d’attente de traitement, et lorsqu’il se termine hello sera disponible à : **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_application\_ID /CK3f0xBF_2bV6wf7gEZE8w.jpg**</span><span class="sxs-lookup"><span data-stu-id="8da44-138">This tells you that Blitline has recieved your request, it has put it in a processing queue, and when it has completed hello image will be available at: **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_APP\_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg**</span></span>

## <a name="how-toosave-an-image-tooyour-azure-storage-account"></a><span data-ttu-id="8da44-139">Comment toosave un tooyour image du compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="8da44-139">How toosave an image tooyour Azure Storage account</span></span>
<span data-ttu-id="8da44-140">Si vous avez un compte de stockage Azure, vous pouvez facilement avoir Blitline les images de hello traitée par émission de données dans votre conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="8da44-140">If you have an Azure Storage account, you can easily have Blitline push hello processed images into your Azure container.</span></span> <span data-ttu-id="8da44-141">En ajoutant un « azure_destination », vous définissez les emplacement hello et les autorisations de toopush Blitline à.</span><span class="sxs-lookup"><span data-stu-id="8da44-141">By adding an "azure_destination" you define hello location and permissions for Blitline toopush to.</span></span>

<span data-ttu-id="8da44-142">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="8da44-142">Here is an example:</span></span>

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


<span data-ttu-id="8da44-143">En renseignant les valeurs hello CAPITALIZED avec votre propre, vous pouvez soumettre cette toohttp://api.blitline.com/job JSON et hello « src » image sera traitée avec un filtre Flou et puis envoyées tooyou destination Azure.</span><span class="sxs-lookup"><span data-stu-id="8da44-143">By filling in hello CAPITALIZED values with your own, you can submit this JSON toohttp://api.blitline.com/job and hello "src" image will be processed with a blur filter and then pushed tooyou Azure destination.</span></span>

### <a name="please-note"></a><span data-ttu-id="8da44-144">Notez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="8da44-144">Please note:</span></span>
<span data-ttu-id="8da44-145">Hello SAS doit contenir l’url SAS entière hello, y compris hello de nom de fichier du fichier de destination hello.</span><span class="sxs-lookup"><span data-stu-id="8da44-145">hello SAS must contain hello entire SAS url, including hello filename of hello destination file.</span></span>

<span data-ttu-id="8da44-146">Exemple :</span><span class="sxs-lookup"><span data-stu-id="8da44-146">Example:</span></span>

    http://blitline.blob.core.windows.net/sample/image.jpg?sr=b&sv=2012-02-12&st=2013-04-12T03%3A18%3A30Z&se=2013-04-12T04%3A18%3A30Z&sp=w&sig=Bte2hkkbwTT2sqlkkKLop2asByrE0sIfeesOwj7jNA5o%3D


<span data-ttu-id="8da44-147">Vous pouvez également lire hello dernière édition de documents de stockage Azure de Blitline [ici](http://www.blitline.com/docs/azure_storage).</span><span class="sxs-lookup"><span data-stu-id="8da44-147">You can also read hello latest edition of Blitline's Azure Storage docs [here](http://www.blitline.com/docs/azure_storage).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8da44-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8da44-148">Next Steps</span></span>
<span data-ttu-id="8da44-149">Visitez tooread blitline.com sur nos autres fonctionnalités :</span><span class="sxs-lookup"><span data-stu-id="8da44-149">Visit blitline.com tooread about all our other features:</span></span>

* <span data-ttu-id="8da44-150">Documents de point de terminaison d'API Blitline <http://www.blitline.com/docs/api></span><span class="sxs-lookup"><span data-stu-id="8da44-150">Blitline API Endpoint Docs <http://www.blitline.com/docs/api></span></span>
* <span data-ttu-id="8da44-151">Fonctions d'API Blitline <http://www.blitline.com/docs/functions></span><span class="sxs-lookup"><span data-stu-id="8da44-151">Blitline API Functions <http://www.blitline.com/docs/functions></span></span>
* <span data-ttu-id="8da44-152">Exemples d'API Blitline <http://www.blitline.com/docs/examples></span><span class="sxs-lookup"><span data-stu-id="8da44-152">Blitline API Examples <http://www.blitline.com/docs/examples></span></span>
* <span data-ttu-id="8da44-153">Bibliothèque Nuget tierce <http://nuget.org/packages/Blitline.Net></span><span class="sxs-lookup"><span data-stu-id="8da44-153">Third Part Nuget Library <http://nuget.org/packages/Blitline.Net></span></span>

