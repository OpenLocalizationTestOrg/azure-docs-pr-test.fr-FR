---
title: "Utiliser des émoticônes Emoji dans Azure Mobile Engagement"
description: "Comment utiliser des émoticônes Emoji dans vos notifications push"
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
ms.openlocfilehash: bbb7ce5e95b229a7505c5e97b6866d5a302a1d27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-emoji-emoticon-within-push-notifications"></a><span data-ttu-id="70ed2-103">Utiliser l’émoticône Emoji dans les notifications push</span><span class="sxs-lookup"><span data-stu-id="70ed2-103">Use Emoji emoticon within Push Notifications</span></span>
<span data-ttu-id="70ed2-104">Vous pouvez inclure des émoticônes Emoji dans votre notification Push en quelques étapes simples :</span><span class="sxs-lookup"><span data-stu-id="70ed2-104">You can include Emoji emoticons in you push notification in a few easy steps:</span></span> 

1. <span data-ttu-id="70ed2-105">Recherchez d’abord l’Emoji à insérer dans le message.</span><span class="sxs-lookup"><span data-stu-id="70ed2-105">First of all you need to find the Emoji you want to send in the message.</span></span> <span data-ttu-id="70ed2-106">Veillez à ce qu’elle soit prise en charge par l’appareil cible. En effet, l’ajout d’émoticônes Emoji nouvellement approuvées aux plateformes d’appareils peut prendre un certain temps.</span><span class="sxs-lookup"><span data-stu-id="70ed2-106">Please ensure that the Emoji you are selecting will be supported by the target device as device manufactures take some time to add newly approved Emojis to the device platforms.</span></span> 
2. <span data-ttu-id="70ed2-107">Sur **Windows** : vous pouvez accéder à ce [lien](http://apps.timwhitlock.info/emoji/tables/unicode) et copier l’icône « Native ».</span><span class="sxs-lookup"><span data-stu-id="70ed2-107">On **Windows** - you can navigate to this [link](http://apps.timwhitlock.info/emoji/tables/unicode) and copy the 'Native' icon.</span></span>
   
    ![][7] 
3. <span data-ttu-id="70ed2-108">Sur **Mac** : les émoticônes Emoji se trouvent dans l’application Dictionnaire sous Modifier -> Emoji et symboles.</span><span class="sxs-lookup"><span data-stu-id="70ed2-108">On **Mac** - you can find the Emojis in Dictionary application under Edit -> Emoji & Symbols.</span></span>
   
    ![][6] 
4. <span data-ttu-id="70ed2-109">Accédez à l’onglet **Reach** du portail Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="70ed2-109">Now, go to the **Reach** tab on the the Azure Mobile Engagement portal.</span></span> <span data-ttu-id="70ed2-110">Sélectionnez le type de votre notification push (annonce, interrogation, etc.).</span><span class="sxs-lookup"><span data-stu-id="70ed2-110">Select the type of your push notification (Announcement, polls etc).</span></span> <span data-ttu-id="70ed2-111">Pour cet exemple, nous choisissons une annonce push.</span><span class="sxs-lookup"><span data-stu-id="70ed2-111">For this example we choose an announcement push.</span></span>
5. <span data-ttu-id="70ed2-112">Spécifiez les différents champs de la notification jusqu'à ce que vous atteigniez le texte de la notification.</span><span class="sxs-lookup"><span data-stu-id="70ed2-112">Specify the different fields of the notification until you reach the text of the notification.</span></span> <span data-ttu-id="70ed2-113">C’est là que vous allez ajouter votre émoticône Emoji.</span><span class="sxs-lookup"><span data-stu-id="70ed2-113">This is where you will add your Emoji Emoticon.</span></span> <span data-ttu-id="70ed2-114">Vous pouvez la placer dans le titre, dans le message ou les deux.</span><span class="sxs-lookup"><span data-stu-id="70ed2-114">You can choose to put it in the title, the message, or both.</span></span> <span data-ttu-id="70ed2-115">Faites glisser-déplacer ou copiez les émoticônes Emoji figurant dans les emplacements ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="70ed2-115">You will need to drag and drop or copy the Emoji that you find from the locations above.</span></span> 
   
    ![][1]
6. <span data-ttu-id="70ed2-116">Renseignez les autres champs de la notification et enregistrez-la.</span><span class="sxs-lookup"><span data-stu-id="70ed2-116">Complete the other fields for the notification and save it.</span></span> 
7. <span data-ttu-id="70ed2-117">Lorsque vous exécutez un test ou activez l'annonce, une notification s’affiche avec l'émoticône spécifiée.</span><span class="sxs-lookup"><span data-stu-id="70ed2-117">When you run a test or activate the announcement you will see a notification with the emoticon as specified.</span></span>   
   
    <span data-ttu-id="70ed2-118">![][3] ![][4] ![][5]</span><span class="sxs-lookup"><span data-stu-id="70ed2-118">![][3] ![][4] ![][5]</span></span>

<!-- Images. -->
[1]: ./media/mobile-engagement-use-emoji-with-push/notification_input.png
[3]: ./media/mobile-engagement-use-emoji-with-push/iOS_Emoji.png
[4]: ./media/mobile-engagement-use-emoji-with-push/Android_Emoji.png
[5]: ./media/mobile-engagement-use-emoji-with-push/WindowsPhone_Emoji.png
[6]: ./media/mobile-engagement-use-emoji-with-push/Mac_SelectEmoji.png
[7]: ./media/mobile-engagement-use-emoji-with-push/Windows_SelectEmoji.png

