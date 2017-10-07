---
title: aaaTemplates
description: "Cette rubrique décrit les modèles pour les hubs de notification Azure."
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: a41897bb-5b4b-48b2-bfd5-2e3c65edc37e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 0149f0c7473e5a4b952905bc8217582b58db2a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="templates"></a><span data-ttu-id="276c5-103">Modèles</span><span class="sxs-lookup"><span data-stu-id="276c5-103">Templates</span></span>
## <a name="overview"></a><span data-ttu-id="276c5-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="276c5-104">Overview</span></span>
<span data-ttu-id="276c5-105">Les modèles permettent à un client application toospecify hello format exact de notifications hello qu'il veut tooreceive.</span><span class="sxs-lookup"><span data-stu-id="276c5-105">Templates enable a client application toospecify hello exact format of hello notifications it wants tooreceive.</span></span> <span data-ttu-id="276c5-106">À l’aide de modèles, une application peut permettre de différents avantages, notamment hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="276c5-106">Using templates, an app can realize several different benefits, including hello following :</span></span>

* <span data-ttu-id="276c5-107">Un serveur principal non spécifique à une plateforme</span><span class="sxs-lookup"><span data-stu-id="276c5-107">A platform-agnostic backend</span></span>
* <span data-ttu-id="276c5-108">Des notifications personnalisées</span><span class="sxs-lookup"><span data-stu-id="276c5-108">Personalized notifications</span></span>
* <span data-ttu-id="276c5-109">Indépendance vis-à-vis de la version du client</span><span class="sxs-lookup"><span data-stu-id="276c5-109">Client-version independence</span></span>
* <span data-ttu-id="276c5-110">Localisation facile</span><span class="sxs-lookup"><span data-stu-id="276c5-110">Easy localization</span></span>

<span data-ttu-id="276c5-111">Cette section fournit deux exemples complets de comment toouse modèles toosend indépendant de la plateforme des notifications ciblant tous vos appareils plates-formes et toopersonalize diffusion tooeach de périphérique de notification.</span><span class="sxs-lookup"><span data-stu-id="276c5-111">This section provides two in-depth examples of how toouse templates toosend platform-agnostic notifications targeting all your devices across platforms, and toopersonalize broadcast notification tooeach device.</span></span>

## <a name="using-templates-cross-platform"></a><span data-ttu-id="276c5-112">Utilisation des modèles entre plateformes</span><span class="sxs-lookup"><span data-stu-id="276c5-112">Using templates cross-platform</span></span>
<span data-ttu-id="276c5-113">notifications de push toosend Hello moyen standard est toosend, pour chaque notification qui est toobe envoyée, une charge utile tooplatform notification les services (WNS, APNS).</span><span class="sxs-lookup"><span data-stu-id="276c5-113">hello standard way toosend push notifications is toosend, for each notification that is toobe sent, a specific payload tooplatform notification services (WNS, APNS).</span></span> <span data-ttu-id="276c5-114">Par exemple, une alerte tooAPNS, de toosend charge utile de hello est un objet Json de hello suivant du formulaire :</span><span class="sxs-lookup"><span data-stu-id="276c5-114">For example, toosend an alert tooAPNS, hello payload is a Json object of hello following form:</span></span>

    {"aps": {"alert" : "Hello!" }}

<span data-ttu-id="276c5-115">toosend un message toast similaire sur une application du Windows Store, charge XML hello est comme suit :</span><span class="sxs-lookup"><span data-stu-id="276c5-115">toosend a similar toast message on a Windows Store application, hello XML payload is as follows:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">Hello!</text>
        </binding>
      </visual>
    </toast>

<span data-ttu-id="276c5-116">Vous pouvez créer des charges utiles similaires pour les plateformes MPNS (Windows Phone) et GCM (Android).</span><span class="sxs-lookup"><span data-stu-id="276c5-116">You can create similar payloads for MPNS (Windows Phone) and GCM (Android) platforms.</span></span>

<span data-ttu-id="276c5-117">Cette exigence force hello application back-end tooproduce différentes charges utiles pour chaque plateforme et le rend hello principal responsable de la partie de la couche de présentation de hello d’application hello.</span><span class="sxs-lookup"><span data-stu-id="276c5-117">This requirement forces hello app backend tooproduce different payloads for each platform, and effectively makes hello backend responsible for part of hello presentation layer of hello app.</span></span> <span data-ttu-id="276c5-118">Certaines préoccupations concernent les présentations graphiques et la localisation (en particulier pour les applications Windows Store qui incluent des notifications pour divers types de mosaïques).</span><span class="sxs-lookup"><span data-stu-id="276c5-118">Some concerns include localization and graphical layouts (especially for Windows Store apps that include notifications for various types of tiles).</span></span>

<span data-ttu-id="276c5-119">fonctionnalité de modèle de Notification Hubs Hello permet à une application toocreate spécial inscriptions des clients, appelé inscriptions de modèle, y compris, en outre ensemble toohello de balises, un modèle.</span><span class="sxs-lookup"><span data-stu-id="276c5-119">hello Notification Hubs template feature enables a client app toocreate special registrations, called template registrations, which include, in addition toohello set of tags, a template.</span></span> <span data-ttu-id="276c5-120">fonctionnalité de modèle de Notification Hubs Hello permet des périphériques client application tooassociate avec des modèles si vous travaillez avec des Installations (recommandées) ou les enregistrements.</span><span class="sxs-lookup"><span data-stu-id="276c5-120">hello Notification Hubs template feature enables a client app tooassociate devices with templates whether you are working with Installations (preferred) or Registrations.</span></span> <span data-ttu-id="276c5-121">Étant donné hello précédant les exemples de la charge utile, hello uniquement les informations indépendant de la plateforme sont message d’alerte réel hello (Hello).</span><span class="sxs-lookup"><span data-stu-id="276c5-121">Given hello preceding payload examples, hello only platform-independent information is hello actual alert message (Hello!).</span></span> <span data-ttu-id="276c5-122">Un modèle est un ensemble d’instructions pour hello Hub de Notification sur comment tooformat indépendant de la plateforme de message pour l’inscription de hello de cette application de client spécifique.</span><span class="sxs-lookup"><span data-stu-id="276c5-122">A template is a set of instructions for hello Notification Hub on how tooformat a platform-independent message for hello registration of that specific client app.</span></span> <span data-ttu-id="276c5-123">Bonjour précédent exemple, message de salutation plateforme indépendant est une propriété unique : **message = Hello !**.</span><span class="sxs-lookup"><span data-stu-id="276c5-123">In hello preceding example, hello platform independent message is a single property: **message = Hello!**.</span></span>

<span data-ttu-id="276c5-124">Hello illustration suivante décrit hello au-dessus de processus :</span><span class="sxs-lookup"><span data-stu-id="276c5-124">hello following picture illustrates hello above process:</span></span>

![](./media/notification-hubs-templates/notification-hubs-hello.png)

<span data-ttu-id="276c5-125">modèle Hello pour l’inscription d’une application cliente iOS hello est comme suit :</span><span class="sxs-lookup"><span data-stu-id="276c5-125">hello template for hello iOS client app registration is as follows:</span></span>

    {"aps": {"alert": "$(message)"}}

<span data-ttu-id="276c5-126">modèle de Hello correspondant pour l’application de client hello du Windows Store est la suivante :</span><span class="sxs-lookup"><span data-stu-id="276c5-126">hello corresponding template for hello Windows Store client app is:</span></span>

    <toast>
        <visual>
            <binding template=\"ToastText01\">
                <text id=\"1\">$(message)</text>
            </binding>
        </visual>
    </toast>

<span data-ttu-id="276c5-127">Notez que hello réel du message est remplacé par hello expression $(message).</span><span class="sxs-lookup"><span data-stu-id="276c5-127">Notice that hello actual message is substituted for hello expression $(message).</span></span> <span data-ttu-id="276c5-128">Cette expression indique hello concentrateur de Notification, chaque fois qu’il envoie un message toothis enregistrement particulier, toobuild un message qui suit il et les commutateurs dans la valeur courante hello.</span><span class="sxs-lookup"><span data-stu-id="276c5-128">This expression instructs hello Notification Hub, whenever it sends a message toothis particular registration, toobuild a message that follows it and switches in hello common value.</span></span>

<span data-ttu-id="276c5-129">Si vous travaillez avec un modèle d’Installation, clé « modèles » de l’installation hello conserve un JSON de plusieurs modèles.</span><span class="sxs-lookup"><span data-stu-id="276c5-129">If you are working with Installation model, hello installation “templates” key holds a JSON of multiple templates.</span></span> <span data-ttu-id="276c5-130">Si vous travaillez avec un modèle d’inscription, hello application cliente peut créer plusieurs enregistrements dans l’ordre toouse plusieurs modèles ; par exemple, un modèle pour les messages d’alerte et un modèle pour les mises à jour de la vignette.</span><span class="sxs-lookup"><span data-stu-id="276c5-130">If you are working with Registration model, hello client application can create multiple registrations in order toouse multiple templates; for example, a template for alert messages and a template for tile updates.</span></span> <span data-ttu-id="276c5-131">Les applications clientes peuvent également combiner inscriptions natives (inscriptions sans modèle) et inscriptions avec modèle.</span><span class="sxs-lookup"><span data-stu-id="276c5-131">Client applications can also mix native registrations (registrations with no template) and template registrations.</span></span>

<span data-ttu-id="276c5-132">Hello Hub de Notification envoie une notification pour chaque modèle sans tenir compte si elles appartiennent toohello même application cliente.</span><span class="sxs-lookup"><span data-stu-id="276c5-132">hello Notification Hub sends one notification for each template without considering whether they belong toohello same client app.</span></span> <span data-ttu-id="276c5-133">Ce comportement peut être utilisé tootranslate des notifications d’indépendant de la plateforme en plus des notifications.</span><span class="sxs-lookup"><span data-stu-id="276c5-133">This behavior can be used tootranslate platform-independent notifications into more notifications.</span></span> <span data-ttu-id="276c5-134">Par exemple, hello même toohello message indépendant de plateforme que Hub de Notification peut être traduit en toute transparence une alerte de toast et une mise à jour de la vignette, sans nécessiter de hello toobe principal prenant en charge de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="276c5-134">For example, hello same platform independent message toohello Notification Hub can be seamlessly translated in a toast alert and a tile update, without requiring hello backend toobe aware of it.</span></span> <span data-ttu-id="276c5-135">Notez que certaines plateformes (par exemple, iOS) peuvent réduire plusieurs notifications toohello appareil même si elles sont envoyées sur une courte période de temps.</span><span class="sxs-lookup"><span data-stu-id="276c5-135">Note that some platforms (for example, iOS) might collapse multiple notifications toohello same device if they are sent in a short period of time.</span></span>

## <a name="using-templates-for-personalization"></a><span data-ttu-id="276c5-136">Utilisation des modèles à des fins de personnalisation</span><span class="sxs-lookup"><span data-stu-id="276c5-136">Using templates for personalization</span></span>
<span data-ttu-id="276c5-137">Modèles de toousing un autre avantage est hello capacité toouse personnalisation de l’inscription par tooperform concentrateurs de Notification des notifications.</span><span class="sxs-lookup"><span data-stu-id="276c5-137">Another advantage toousing templates is hello ability toouse Notification Hubs tooperform per-registration personalization of notifications.</span></span> <span data-ttu-id="276c5-138">Par exemple, considérez une application Météo qui affiche une vignette avec les conditions météo hello à un emplacement spécifique.</span><span class="sxs-lookup"><span data-stu-id="276c5-138">For example, consider a weather app that displays a tile with hello weather conditions at a specific location.</span></span> <span data-ttu-id="276c5-139">Un utilisateur peut choisir entre les degrés Celsius ou Fahrenheit, et une prévision à un jour ou sur les cinq prochains jours.</span><span class="sxs-lookup"><span data-stu-id="276c5-139">A user can choose between Celsius or Fahrenheit degrees, and a single or five-day forecast.</span></span> <span data-ttu-id="276c5-140">À l’aide de modèles, chaque installation de l’application cliente peut inscrire pour format hello requis (1 jour Fahrenheit Celsius, 1 jour, 5 jours Celsius, 5 jours Fahrenheit), et avoir hello principal d’envoyer un message unique qui contient toutes les informations de hello requis toofill celles modèles (par exemple, une cinq jours prévision avec degrés Celsius et Fahrenheit).</span><span class="sxs-lookup"><span data-stu-id="276c5-140">Using templates, each client app installation can register for hello format required (1-day Celsius, 1-day Fahrenheit, 5-days Celsius, 5-days Fahrenheit), and have hello backend send a single message that contains all hello information required toofill those templates (for example, a five-day forecast with Celsius and Fahrenheit degrees).</span></span>

<span data-ttu-id="276c5-141">modèle de Hello pour hello une journée prévision avec Celsius températures est comme suit :</span><span class="sxs-lookup"><span data-stu-id="276c5-141">hello template for hello one-day forecast with Celsius temperatures is as follows:</span></span>

    <tile>
      <visual>
        <binding template="TileWideSmallImageAndText04">
          <image id="1" src="$(day1_image)" alt="alt text"/>
          <text id="1">Seattle, WA</text>
          <text id="2">$(day1_tempC)</text>
        </binding>  
      </visual>
    </tile>

<span data-ttu-id="276c5-142">message envoyé de Hello toohello Hub de Notification contient hello toutes les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="276c5-142">hello message sent toohello Notification Hub contains all hello following properties:</span></span>

<table border="1">

<tr><td><span data-ttu-id="276c5-143">day1_image</span><span class="sxs-lookup"><span data-stu-id="276c5-143">day1_image</span></span></td><td><span data-ttu-id="276c5-144">day2_image</span><span class="sxs-lookup"><span data-stu-id="276c5-144">day2_image</span></span></td><td><span data-ttu-id="276c5-145">day3_image</span><span class="sxs-lookup"><span data-stu-id="276c5-145">day3_image</span></span></td><td><span data-ttu-id="276c5-146">day4_image</span><span class="sxs-lookup"><span data-stu-id="276c5-146">day4_image</span></span></td><td><span data-ttu-id="276c5-147">day5_image</span><span class="sxs-lookup"><span data-stu-id="276c5-147">day5_image</span></span></td></tr>

<tr><td><span data-ttu-id="276c5-148">day1_tempC</span><span class="sxs-lookup"><span data-stu-id="276c5-148">day1_tempC</span></span></td><td><span data-ttu-id="276c5-149">day2_tempC</span><span class="sxs-lookup"><span data-stu-id="276c5-149">day2_tempC</span></span></td><td><span data-ttu-id="276c5-150">day3_tempC</span><span class="sxs-lookup"><span data-stu-id="276c5-150">day3_tempC</span></span></td><td><span data-ttu-id="276c5-151">day4_tempC</span><span class="sxs-lookup"><span data-stu-id="276c5-151">day4_tempC</span></span></td><td><span data-ttu-id="276c5-152">day5_tempC</span><span class="sxs-lookup"><span data-stu-id="276c5-152">day5_tempC</span></span></td></tr>

<tr><td><span data-ttu-id="276c5-153">day1_tempF</span><span class="sxs-lookup"><span data-stu-id="276c5-153">day1_tempF</span></span></td><td><span data-ttu-id="276c5-154">day2_tempF</span><span class="sxs-lookup"><span data-stu-id="276c5-154">day2_tempF</span></span></td><td><span data-ttu-id="276c5-155">day3_tempF</span><span class="sxs-lookup"><span data-stu-id="276c5-155">day3_tempF</span></span></td><td><span data-ttu-id="276c5-156">day4_tempF</span><span class="sxs-lookup"><span data-stu-id="276c5-156">day4_tempF</span></span></td><td><span data-ttu-id="276c5-157">day5_tempF</span><span class="sxs-lookup"><span data-stu-id="276c5-157">day5_tempF</span></span></td></tr>
</table><br/>

<span data-ttu-id="276c5-158">À l’aide de ce modèle, hello principal envoie uniquement un seul message sans avoir toostore les options de personnalisation spécifiques pour les utilisateurs d’application hello.</span><span class="sxs-lookup"><span data-stu-id="276c5-158">By using this pattern, hello backend only sends a single message without having toostore specific personalization options for hello app users.</span></span> <span data-ttu-id="276c5-159">Hello illustration suivante décrit ce scénario :</span><span class="sxs-lookup"><span data-stu-id="276c5-159">hello following picture illustrates this scenario:</span></span>

![](./media/notification-hubs-templates/notification-hubs-registration-specific.png)

## <a name="how-tooregister-templates"></a><span data-ttu-id="276c5-160">Comment les modèles tooregister</span><span class="sxs-lookup"><span data-stu-id="276c5-160">How tooregister templates</span></span>
<span data-ttu-id="276c5-161">tooregister avec des modèles à l’aide du modèle d’Installation hello (recommandé) ou hello modèle d’inscription, consultez [gestion de l’inscription](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="276c5-161">tooregister with templates using hello Installation model (preferred), or hello Registration model, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

## <a name="template-expression-language"></a><span data-ttu-id="276c5-162">Langage d’expression de modèle</span><span class="sxs-lookup"><span data-stu-id="276c5-162">Template expression language</span></span>
<span data-ttu-id="276c5-163">Les modèles sont tooXML limité ou formats de documents JSON.</span><span class="sxs-lookup"><span data-stu-id="276c5-163">Templates are limited tooXML or JSON document formats.</span></span> <span data-ttu-id="276c5-164">Vous pouvez également placer des expressions à des endroits particuliers ; par exemple, des attributs de nœud ou des valeurs pour XML, des valeurs de propriété de chaîne pour JSON.</span><span class="sxs-lookup"><span data-stu-id="276c5-164">Also, you can only place expressions in particular places; for example, node attributes or values for XML, string property values for JSON.</span></span>

<span data-ttu-id="276c5-165">Hello tableau suivant affiche langage hello autorisée dans les modèles :</span><span class="sxs-lookup"><span data-stu-id="276c5-165">hello following table shows hello language allowed in templates:</span></span>

| <span data-ttu-id="276c5-166">Expression</span><span class="sxs-lookup"><span data-stu-id="276c5-166">Expression</span></span> | <span data-ttu-id="276c5-167">Description</span><span class="sxs-lookup"><span data-stu-id="276c5-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="276c5-168">$(prop)</span><span class="sxs-lookup"><span data-stu-id="276c5-168">$(prop)</span></span> |<span data-ttu-id="276c5-169">Propriété d’événement tooan référence avec le nom donné de hello.</span><span class="sxs-lookup"><span data-stu-id="276c5-169">Reference tooan event property with hello given name.</span></span> <span data-ttu-id="276c5-170">Les noms de propriétés ne respectent pas la casse.</span><span class="sxs-lookup"><span data-stu-id="276c5-170">Property names are not case-sensitive.</span></span> <span data-ttu-id="276c5-171">Cette expression est résolue en valeur de texte de la propriété hello ou dans une chaîne vide si la propriété de hello n’est pas présente.</span><span class="sxs-lookup"><span data-stu-id="276c5-171">This expression resolves into hello property’s text value or into an empty string if hello property is not present.</span></span> |
| <span data-ttu-id="276c5-172">$(prop, n)</span><span class="sxs-lookup"><span data-stu-id="276c5-172">$(prop, n)</span></span> |<span data-ttu-id="276c5-173">Comme ci-dessus, mais hello texte est explicitement tronqué sur n caractères, par exemple $(titre, 20) découpe hello contenu de la propriété de titre hello à 20 caractères.</span><span class="sxs-lookup"><span data-stu-id="276c5-173">As above, but hello text is explicitly clipped at n characters, for example $(title, 20) clips hello contents of hello title property at 20 characters.</span></span> |
| <span data-ttu-id="276c5-174">.(prop, n)</span><span class="sxs-lookup"><span data-stu-id="276c5-174">.(prop, n)</span></span> |<span data-ttu-id="276c5-175">Comme ci-dessus, mais hello texte est suivi du suffixe avec trois points comme il est tronqué.</span><span class="sxs-lookup"><span data-stu-id="276c5-175">As above, but hello text is suffixed with three dots as it is clipped.</span></span> <span data-ttu-id="276c5-176">taille totale de Hello Hello détouré chaîne et suffixe de hello ne dépasse pas n caractères.</span><span class="sxs-lookup"><span data-stu-id="276c5-176">hello total size of hello clipped string and hello suffix does not exceed n characters.</span></span> <span data-ttu-id="276c5-177">. (titre, 20) avec une propriété d’entrée de « This is ligne de titre hello » entraîne **ce titre de hello est en cours...**</span><span class="sxs-lookup"><span data-stu-id="276c5-177">.(title, 20) with an input property of “This is hello title line” results in **This is hello title...**</span></span> |
| <span data-ttu-id="276c5-178">%(prop)</span><span class="sxs-lookup"><span data-stu-id="276c5-178">%(prop)</span></span> |<span data-ttu-id="276c5-179">Too$(name) similaire à l’exception de cette sortie hello est codée au format URI.</span><span class="sxs-lookup"><span data-stu-id="276c5-179">Similar too$(name) except that hello output is URI-encoded.</span></span> |
| <span data-ttu-id="276c5-180">#(prop)</span><span class="sxs-lookup"><span data-stu-id="276c5-180">#(prop)</span></span> |<span data-ttu-id="276c5-181">Utilisé dans les modèles JSON (par exemple, pour les modèles iOS et Android).</span><span class="sxs-lookup"><span data-stu-id="276c5-181">Used in JSON templates (for example, for iOS and Android templates).</span></span><br><br><span data-ttu-id="276c5-182">Cette fonction est effective même hello exactement comme $(prop) précédemment spécifié, sauf lorsque utilisés dans les modèles JSON (par exemple, les modèles d’Apple).</span><span class="sxs-lookup"><span data-stu-id="276c5-182">This function works exactly hello same as $(prop) previously specified, except when used in JSON templates (for example, Apple templates).</span></span> <span data-ttu-id="276c5-183">Dans ce cas, si cette fonction n’est pas entourée par des « {', '} » (par exemple, 'myJsonProperty' : « #(nom) »), et il a la valeur nombre tooa au format Javascript, par exemple, regexp : (0 &#124; (&#91; 1-9 &#93; &#91; 0-9 & #93  ;*))(\. &#91; 0-9 &#93; +) ? ((e &#124; E) (+ &#124;-) ? &#91; 0-9 &#93; +) ?, puis hello de sortie JSON est un nombre.</span><span class="sxs-lookup"><span data-stu-id="276c5-183">In this case, if this function is not surrounded by “{‘,’}” (for example, ‘myJsonProperty’ : ‘#(name)’), and it evaluates tooa number in Javascript format, for example, regexp: (0&#124;(&#91;1-9&#93;&#91;0-9&#93;*))(\.&#91;0-9&#93;+)?((e&#124;E)(+&#124;-)?&#91;0-9&#93;+)?, then hello output JSON is a number.</span></span><br><br><span data-ttu-id="276c5-184">Par exemple, 'badge : '#(name)' devient 'badge' : 40 (et non '40').</span><span class="sxs-lookup"><span data-stu-id="276c5-184">For example, ‘badge : ‘#(name)’ becomes ‘badge’ : 40 (and not ‘40‘).</span></span> |
| <span data-ttu-id="276c5-185">‘text’ ou « text »</span><span class="sxs-lookup"><span data-stu-id="276c5-185">‘text’ or “text”</span></span> |<span data-ttu-id="276c5-186">Un littéral.</span><span class="sxs-lookup"><span data-stu-id="276c5-186">A literal.</span></span> <span data-ttu-id="276c5-187">Les littéraux contiennent du texte arbitraire placé entre guillemets simples ou doubles.</span><span class="sxs-lookup"><span data-stu-id="276c5-187">Literals contain arbitrary text enclosed in single or double quotes.</span></span> |
| <span data-ttu-id="276c5-188">expr1 + expr2</span><span class="sxs-lookup"><span data-stu-id="276c5-188">expr1 + expr2</span></span> |<span data-ttu-id="276c5-189">opérateur de concaténation Hello jointure de deux expressions en une seule chaîne.</span><span class="sxs-lookup"><span data-stu-id="276c5-189">hello concatenation operator joining two expressions into a single string.</span></span> |

<span data-ttu-id="276c5-190">les expressions Hello peuvent être hello précédant les formulaires.</span><span class="sxs-lookup"><span data-stu-id="276c5-190">hello expressions can be any of hello preceding forms.</span></span>

<span data-ttu-id="276c5-191">Lors de l’utilisation de la concaténation, ensemble de l’expression hello doit être entouré de {}.</span><span class="sxs-lookup"><span data-stu-id="276c5-191">When using concatenation, hello entire expression must be surrounded with {}.</span></span> <span data-ttu-id="276c5-192">Par exemple, {$(prop) + ' - ' + $(prop2)}.</span><span class="sxs-lookup"><span data-stu-id="276c5-192">For example, {$(prop) + ‘ - ’ + $(prop2)}.</span></span> |

<span data-ttu-id="276c5-193">Par exemple, suivant de hello n’est pas un modèle XML valide :</span><span class="sxs-lookup"><span data-stu-id="276c5-193">For example, hello following is not a valid XML template:</span></span>

    <tile>
      <visual>
        <binding $(property)>
          <text id="1">Seattle, WA</text>
        </binding>  
      </visual>
    </tile>


<span data-ttu-id="276c5-194">Comme expliqué ci-dessus, lors de l’utilisation de la concaténation, les expressions doivent être placées entre accolades.</span><span class="sxs-lookup"><span data-stu-id="276c5-194">As explained above, when using concatenation, expressions must be wrapped in curly brackets.</span></span> <span data-ttu-id="276c5-195">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="276c5-195">For example:</span></span>

    <tile>
      <visual>
        <binding template="ToastText01">
          <text id="1">{'Hi, ' + $(name)}</text>
        </binding>  
      </visual>
    </tile>

