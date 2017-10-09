---
title: "aaaUse des émoticônes Emoji dans Azure Mobile Engagement"
description: "Comment toouse des émoticônes Emoji dans vos notifications push"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 663317d7-3c93-4e8f-b13d-c6fb342124ee
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 63bfc59ef472e9fe9aa28b5ac8761017b9250e0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-emoji-emoticon-within-push-notifications"></a><span data-ttu-id="f1f7d-103">Utiliser l’émoticône Emoji dans les notifications push</span><span class="sxs-lookup"><span data-stu-id="f1f7d-103">Use Emoji emoticon within Push Notifications</span></span>
<span data-ttu-id="f1f7d-104">Vous pouvez inclure des émoticônes Emoji dans votre notification Push en quelques étapes simples :</span><span class="sxs-lookup"><span data-stu-id="f1f7d-104">You can include Emoji emoticons in you push notification in a few easy steps:</span></span> 

1. <span data-ttu-id="f1f7d-105">Tout d’abord, vous devez toofind hello Emoji souhaité toosend dans le message de type hello.</span><span class="sxs-lookup"><span data-stu-id="f1f7d-105">First of all you need toofind hello Emoji you want toosend in hello message.</span></span> <span data-ttu-id="f1f7d-106">Vérifiez que hello Emoji que vous sélectionnez sera pris en charge par le périphérique cible de hello comme les fabricants de périphériques prennent certaines tooadd temps des plateformes d’appareils toohello Emojis qui vient d’être approuvées.</span><span class="sxs-lookup"><span data-stu-id="f1f7d-106">Please ensure that hello Emoji you are selecting will be supported by hello target device as device manufactures take some time tooadd newly approved Emojis toohello device platforms.</span></span> 
2. <span data-ttu-id="f1f7d-107">Sur **Windows** -vous pouvez naviguer toothis [lien](http://apps.timwhitlock.info/emoji/tables/unicode) et l’icône de copie hello 'Native'.</span><span class="sxs-lookup"><span data-stu-id="f1f7d-107">On **Windows** - you can navigate toothis [link](http://apps.timwhitlock.info/emoji/tables/unicode) and copy hello 'Native' icon.</span></span>
   
    ![][7] 
3. <span data-ttu-id="f1f7d-108">Sur **Mac** -vous pouvez trouver hello Emojis dans une application de type dictionnaire sous Modifier -> Emoji et symboles.</span><span class="sxs-lookup"><span data-stu-id="f1f7d-108">On **Mac** - you can find hello Emojis in Dictionary application under Edit -> Emoji & Symbols.</span></span>
   
    ![][6] 
4. <span data-ttu-id="f1f7d-109">Passez maintenant toohello **atteindre** onglet sur le portail Azure Mobile Engagement hello hello.</span><span class="sxs-lookup"><span data-stu-id="f1f7d-109">Now, go toohello **Reach** tab on hello hello Azure Mobile Engagement portal.</span></span> <span data-ttu-id="f1f7d-110">Sélectionnez le type hello votre notification push (annonce, sondages, etc.).</span><span class="sxs-lookup"><span data-stu-id="f1f7d-110">Select hello type of your push notification (Announcement, polls etc).</span></span> <span data-ttu-id="f1f7d-111">Pour cet exemple, nous choisissons une annonce push.</span><span class="sxs-lookup"><span data-stu-id="f1f7d-111">For this example we choose an announcement push.</span></span>
5. <span data-ttu-id="f1f7d-112">Spécifiez hello différents champs de notification de hello jusqu'à ce que vous atteigniez texte hello de notification de hello.</span><span class="sxs-lookup"><span data-stu-id="f1f7d-112">Specify hello different fields of hello notification until you reach hello text of hello notification.</span></span> <span data-ttu-id="f1f7d-113">C’est là que vous allez ajouter votre émoticône Emoji.</span><span class="sxs-lookup"><span data-stu-id="f1f7d-113">This is where you will add your Emoji Emoticon.</span></span> <span data-ttu-id="f1f7d-114">Vous pouvez choisir tooput dans le titre de hello, le message de type hello ou les deux.</span><span class="sxs-lookup"><span data-stu-id="f1f7d-114">You can choose tooput it in hello title, hello message, or both.</span></span> <span data-ttu-id="f1f7d-115">Vous devez toodrag et supprimer ou copier hello Emoji que vous trouvez à partir d’emplacements hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="f1f7d-115">You will need toodrag and drop or copy hello Emoji that you find from hello locations above.</span></span> 
   
    ![][1]
6. <span data-ttu-id="f1f7d-116">Complète hello autres champs pour la notification de hello et l’enregistrer.</span><span class="sxs-lookup"><span data-stu-id="f1f7d-116">Complete hello other fields for hello notification and save it.</span></span> 
7. <span data-ttu-id="f1f7d-117">Lorsque vous exécutez un test ou que vous activez l’annonce de type hello vous verrez une notification avec les émoticône hello comme spécifié.</span><span class="sxs-lookup"><span data-stu-id="f1f7d-117">When you run a test or activate hello announcement you will see a notification with hello emoticon as specified.</span></span>   
   
    <span data-ttu-id="f1f7d-118">![][3]![][4]![][5]</span><span class="sxs-lookup"><span data-stu-id="f1f7d-118">![][3] ![][4] ![][5]</span></span>

<!-- Images. -->
[1]: ./media/mobile-engagement-use-emoji-with-push/notification_input.png
[3]: ./media/mobile-engagement-use-emoji-with-push/iOS_Emoji.png
[4]: ./media/mobile-engagement-use-emoji-with-push/Android_Emoji.png
[5]: ./media/mobile-engagement-use-emoji-with-push/WindowsPhone_Emoji.png
[6]: ./media/mobile-engagement-use-emoji-with-push/Mac_SelectEmoji.png
[7]: ./media/mobile-engagement-use-emoji-with-push/Windows_SelectEmoji.png

