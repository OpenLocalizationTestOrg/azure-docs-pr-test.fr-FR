---
title: "Utilisation de Blitline pour le traitement d'image - Guide des fonctionnalités Azure"
description: "Apprenez à utiliser le service Blitline pour traiter les images au sein d'une application Microsoft Azure."
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
ms.openlocfilehash: 1d90599e028b3407a513b04b878e3aefc39928a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-blitline-with-azure-and-azure-storage"></a><span data-ttu-id="86653-103">Utilisation de Blitline avec Azure et Azure Storage</span><span class="sxs-lookup"><span data-stu-id="86653-103">How to use Blitline with Azure and Azure Storage</span></span>
<span data-ttu-id="86653-104">Ce guide explique comment accéder aux services Blitline et comment envoyer des tâches à Blitline.</span><span class="sxs-lookup"><span data-stu-id="86653-104">This guide will explain how to access Blitline services and how to submit jobs to Blitline.</span></span>

## <a name="what-is-blitline"></a><span data-ttu-id="86653-105">Présentation de Blitline</span><span class="sxs-lookup"><span data-stu-id="86653-105">What is Blitline?</span></span>
<span data-ttu-id="86653-106">Blitline est un service de traitement d'image sur le cloud. Il offre un traitement d'image de niveau entreprise pour un prix dérisoire par rapport à ce qu'il vous en coûterait si vous le génériez vous-même.</span><span class="sxs-lookup"><span data-stu-id="86653-106">Blitline is a cloud-based image processing service that provides enterprise level image processing at a fraction of the price that it would cost to build it yourself.</span></span>

<span data-ttu-id="86653-107">Le traitement d'image s'effectue à de très nombreuses reprises. Il est généralement intégralement reconçu pour chaque site Web.</span><span class="sxs-lookup"><span data-stu-id="86653-107">The fact is that image processing has been done over and over again, usually rebuilt from the ground up for each and every website.</span></span> <span data-ttu-id="86653-108">Nous sommes bien placés pour le savoir, car nous en avons conçu un nombre incalculable de fois.</span><span class="sxs-lookup"><span data-stu-id="86653-108">We realize this because we’ve built them a million times too.</span></span> <span data-ttu-id="86653-109">Un jour, nous avons décidé qu'il était temps de proposer ce service à tout un chacun.</span><span class="sxs-lookup"><span data-stu-id="86653-109">One day we decided that perhaps it‘s time we just do it for everyone.</span></span> <span data-ttu-id="86653-110">Nous savons effectuer cette action, de façon rapide et efficace, afin de faire gagner du temps de travail à tous.</span><span class="sxs-lookup"><span data-stu-id="86653-110">We know how to do it, to do it fast and efficiently, and save everyone work in the meantime.</span></span>

<span data-ttu-id="86653-111">Pour plus d'informations, consultez la page [http://www.blitline.com](http://www.blitline.com).</span><span class="sxs-lookup"><span data-stu-id="86653-111">For more information, see [http://www.blitline.com](http://www.blitline.com).</span></span>

## <a name="what-blitline-is-not"></a><span data-ttu-id="86653-112">Éléments non proposés par Blitline</span><span class="sxs-lookup"><span data-stu-id="86653-112">What Blitline is NOT...</span></span>
<span data-ttu-id="86653-113">Pour clarifier l'utilité de Blitline, il est plus simple d'identifier les éléments non proposés avant de poursuivre.</span><span class="sxs-lookup"><span data-stu-id="86653-113">To clarify what Blitline is useful for, it is often easier to identify what Blitline does NOT do before moving forward.</span></span>

* <span data-ttu-id="86653-114">Blitline ne possède pas de widgets HTML pour le téléchargement d'images.</span><span class="sxs-lookup"><span data-stu-id="86653-114">Blitline does NOT have HTML widgets to upload images.</span></span> <span data-ttu-id="86653-115">Vous devez disposer d'images disponibles publiquement ou avec des droits d'accès restreints pour que Blitline puisse y accéder.</span><span class="sxs-lookup"><span data-stu-id="86653-115">You must have images available publicly or with restricted permissions available for Blitline to reach.</span></span>
* <span data-ttu-id="86653-116">Blitline n'offre pas de traitement d'image en direct, contrairement à Aviary.com.</span><span class="sxs-lookup"><span data-stu-id="86653-116">Blitline does NOT do live image processing, like Aviary.com</span></span>
* <span data-ttu-id="86653-117">Blitline n'accepte pas de téléchargements d'images, vous ne pouvez donc pas envoyer vos images à Blitline directement.</span><span class="sxs-lookup"><span data-stu-id="86653-117">Blitline does NOT accept image uploads, you cannot push your images to Blitline directly.</span></span> <span data-ttu-id="86653-118">Vous devez les placer sur Azure Storage ou d'autres emplacements pris en charge par Blitline, puis indiquer à Blitline où aller les récupérer.</span><span class="sxs-lookup"><span data-stu-id="86653-118">You must push them to Azure Storage or other places Blitline supports and then tell Blitline where to go get them.</span></span>
* <span data-ttu-id="86653-119">Blitline est massivement parallèle et n'effectue pas de traitement synchrone.</span><span class="sxs-lookup"><span data-stu-id="86653-119">Blitline is massively parallel and does NOT do any synchronous processing.</span></span> <span data-ttu-id="86653-120">Vous devez nous fournir une URL de retour et nous vous préviendrons lorsque nous aurons fini le traitement.</span><span class="sxs-lookup"><span data-stu-id="86653-120">Meaning you must give us a postback_url and we can tell you when we are done processing.</span></span>

## <a name="create-a-blitline-account"></a><span data-ttu-id="86653-121">Création d'un compte Blitline</span><span class="sxs-lookup"><span data-stu-id="86653-121">Create a Blitline account</span></span>
[!INCLUDE [blitline-signup](../includes/blitline-signup.md)]

## <a name="how-to-create-a-blitline-job"></a><span data-ttu-id="86653-122">Création d'une tâche Blitline</span><span class="sxs-lookup"><span data-stu-id="86653-122">How to create a Blitline job</span></span>
<span data-ttu-id="86653-123">Blitline utilise JSON pour définir les actions que vous souhaitez effectuer sur une image.</span><span class="sxs-lookup"><span data-stu-id="86653-123">Blitline uses JSON to define the actions you want to take on an image.</span></span> <span data-ttu-id="86653-124">Ce JSON se compose de quelques champs simples.</span><span class="sxs-lookup"><span data-stu-id="86653-124">This JSON is composed of a few simple fields.</span></span>

<span data-ttu-id="86653-125">Vous en trouverez l'exemple le plus simple ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="86653-125">The simplest example is as follows:</span></span>

        json : '{
       "application_id": "MY_APP_ID",
       "src" : "http://cdn.blitline.com/filters/boys.jpeg",
       "functions" : [ {
           "name": "resize_to_fit",
           "params" : { "width": 240, "height": 140 },
           "save" : { "image_identifier" : "external_sample_1" }
       } ]
    }'

<span data-ttu-id="86653-126">Dans cet exemple, JSON prendra une image « src » « ...boys.jpeg » et la redimensionnera au format 240 x 140.</span><span class="sxs-lookup"><span data-stu-id="86653-126">Here we have JSON that will take a "src" image "...boys.jpeg" and then resize that image to 240x140.</span></span>

<span data-ttu-id="86653-127">Vous trouverez l'ID d'application dans votre onglet **INFORMATIONS DE CONNEXION** ou **GÉRER** sur Azure.</span><span class="sxs-lookup"><span data-stu-id="86653-127">The Application ID is something you can find in your **CONNECTION INFO** or **MANAGE** tab on Azure.</span></span> <span data-ttu-id="86653-128">Il s'agit de votre identifiant secret qui vous permet d'exécuter des tâches sur Blitline.</span><span class="sxs-lookup"><span data-stu-id="86653-128">It is your secret identifier that allows you to run jobs on Blitline.</span></span>

<span data-ttu-id="86653-129">Le paramètre « save » identifie les informations relatives à l'endroit où vous souhaitez placer l'image après l'avoir traitée.</span><span class="sxs-lookup"><span data-stu-id="86653-129">The "save" parameter identifies information about where you want to put the image once we have processed it.</span></span> <span data-ttu-id="86653-130">Dans cet exemple sans importance, nous n'avons pas défini d'endroit.</span><span class="sxs-lookup"><span data-stu-id="86653-130">In this trivial case, we haven't defined one.</span></span> <span data-ttu-id="86653-131">Si aucun endroit n'est défini, Blitline la stockera localement (et temporairement) dans un emplacement de cloud unique.</span><span class="sxs-lookup"><span data-stu-id="86653-131">If no location is defined Blitline will store it locally (and temporarily) at a unique cloud location.</span></span> <span data-ttu-id="86653-132">Vous pourrez obtenir cet emplacement grâce au JSON renvoyé par Blitline lorsque vous effectuez le Blitline.</span><span class="sxs-lookup"><span data-stu-id="86653-132">You will be able to get that location from the JSON returned by Blitline when you make the Blitline.</span></span> <span data-ttu-id="86653-133">L'identificateur « image » est requis et vous est renvoyé pour l'identification de cette image sauvegardée particulière.</span><span class="sxs-lookup"><span data-stu-id="86653-133">The "image" identifier is required and is returned to you when to identify this particular saved image.</span></span>

<span data-ttu-id="86653-134">Vous trouverez plus d’informations sur les *fonctions* prises en charge à l’adresse suivante : <http://www.blitline.com/docs/functions></span><span class="sxs-lookup"><span data-stu-id="86653-134">You can find more information about the *functions* we support here: <http://www.blitline.com/docs/functions></span></span>

<span data-ttu-id="86653-135">Vous pouvez également trouver de la documentation sur les options de tâche à l’adresse suivante : <http://www.blitline.com/docs/api></span><span class="sxs-lookup"><span data-stu-id="86653-135">You can also find documentation about the job options here: <http://www.blitline.com/docs/api></span></span>

<span data-ttu-id="86653-136">Lorsque vous avez votre JSON, vous devez simplement le **PUBLIER** sur `http://api.blitline.com/job`.</span><span class="sxs-lookup"><span data-stu-id="86653-136">Once you have your JSON all you need to do is **POST** it to `http://api.blitline.com/job`</span></span>

<span data-ttu-id="86653-137">Le JSON renvoyé ressemblera à ceci :</span><span class="sxs-lookup"><span data-stu-id="86653-137">You will get JSON back that looks something like this:</span></span>

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


<span data-ttu-id="86653-138">Ceci vous indique que Blitline a reçu votre requête et qu'il l'a placée dans une file d'attente de traitement. Une fois l'image terminée, elle sera disponible à l'adresse suivante : **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_APP\_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg**</span><span class="sxs-lookup"><span data-stu-id="86653-138">This tells you that Blitline has recieved your request, it has put it in a processing queue, and when it has completed the image will be available at: **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_APP\_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg**</span></span>

## <a name="how-to-save-an-image-to-your-azure-storage-account"></a><span data-ttu-id="86653-139">Enregistrement d'une image sur votre compte Azure Storage</span><span class="sxs-lookup"><span data-stu-id="86653-139">How to save an image to your Azure Storage account</span></span>
<span data-ttu-id="86653-140">Si vous possédez un compte Azure Storage, vous pouvez facilement demander à Blitline d'envoyer les images traitées sur votre conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="86653-140">If you have an Azure Storage account, you can easily have Blitline push the processed images into your Azure container.</span></span> <span data-ttu-id="86653-141">En ajoutant un paramètre « azure_destination », vous définissez l'emplacement et les autorisations pour l'envoi par Blitline.</span><span class="sxs-lookup"><span data-stu-id="86653-141">By adding an "azure_destination" you define the location and permissions for Blitline to push to.</span></span>

<span data-ttu-id="86653-142">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="86653-142">Here is an example:</span></span>

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


<span data-ttu-id="86653-143">En remplissant les valeurs EN MAJUSCULE avec vos propres valeurs, vous pouvez envoyer ce JSON à l'adresse http://api.blitline.com/job. L'image « src » sera traitée avec un filtre de flou, puis sera envoyée à votre destination Azure.</span><span class="sxs-lookup"><span data-stu-id="86653-143">By filling in the CAPITALIZED values with your own, you can submit this JSON to http://api.blitline.com/job and the "src" image will be processed with a blur filter and then pushed to you Azure destination.</span></span>

### <a name="please-note"></a><span data-ttu-id="86653-144">Notez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="86653-144">Please note:</span></span>
<span data-ttu-id="86653-145">La SAP doit contenir toute l'adresse SAP, y compris le nom du fichier de destination.</span><span class="sxs-lookup"><span data-stu-id="86653-145">The SAS must contain the entire SAS url, including the filename of the destination file.</span></span>

<span data-ttu-id="86653-146">Exemple :</span><span class="sxs-lookup"><span data-stu-id="86653-146">Example:</span></span>

    http://blitline.blob.core.windows.net/sample/image.jpg?sr=b&sv=2012-02-12&st=2013-04-12T03%3A18%3A30Z&se=2013-04-12T04%3A18%3A30Z&sp=w&sig=Bte2hkkbwTT2sqlkkKLop2asByrE0sIfeesOwj7jNA5o%3D


<span data-ttu-id="86653-147">Vous pouvez également lire la dernière édition des documents Azure Storage de Blitline [ici](http://www.blitline.com/docs/azure_storage).</span><span class="sxs-lookup"><span data-stu-id="86653-147">You can also read the latest edition of Blitline's Azure Storage docs [here](http://www.blitline.com/docs/azure_storage).</span></span>

## <a name="next-steps"></a><span data-ttu-id="86653-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="86653-148">Next Steps</span></span>
<span data-ttu-id="86653-149">Rendez-vous sur blitline.com pour découvrir toutes nos autres fonctions :</span><span class="sxs-lookup"><span data-stu-id="86653-149">Visit blitline.com to read about all our other features:</span></span>

* <span data-ttu-id="86653-150">Documents de point de terminaison d'API Blitline <http://www.blitline.com/docs/api></span><span class="sxs-lookup"><span data-stu-id="86653-150">Blitline API Endpoint Docs <http://www.blitline.com/docs/api></span></span>
* <span data-ttu-id="86653-151">Fonctions d'API Blitline <http://www.blitline.com/docs/functions></span><span class="sxs-lookup"><span data-stu-id="86653-151">Blitline API Functions <http://www.blitline.com/docs/functions></span></span>
* <span data-ttu-id="86653-152">Exemples d'API Blitline <http://www.blitline.com/docs/examples></span><span class="sxs-lookup"><span data-stu-id="86653-152">Blitline API Examples <http://www.blitline.com/docs/examples></span></span>
* <span data-ttu-id="86653-153">Bibliothèque Nuget tierce <http://nuget.org/packages/Blitline.Net></span><span class="sxs-lookup"><span data-stu-id="86653-153">Third Part Nuget Library <http://nuget.org/packages/Blitline.Net></span></span>

