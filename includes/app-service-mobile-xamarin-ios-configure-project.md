#### <a name="configure-hello-ios-project-in-xamarin-studio"></a><span data-ttu-id="60291-101">Configurer le projet d’iOS hello dans Xamarin Studio</span><span class="sxs-lookup"><span data-stu-id="60291-101">Configure hello iOS project in Xamarin Studio</span></span>
1. <span data-ttu-id="60291-102">Dans Xamarin.Studio, ouvrez **Info.plist**et la mise à jour hello **identificateur de lot** avec hello regrouper ID que vous avez créé précédemment avec votre nouvel ID d’application.</span><span class="sxs-lookup"><span data-stu-id="60291-102">In Xamarin.Studio, open **Info.plist**, and update hello **Bundle Identifier** with hello bundle ID that you created earlier with your new app ID.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-21.png)
2. <span data-ttu-id="60291-103">Faites défiler la liste trop**Modes d’arrière-plan**.</span><span class="sxs-lookup"><span data-stu-id="60291-103">Scroll down too**Background Modes**.</span></span> <span data-ttu-id="60291-104">Sélectionnez hello **activer les Modes d’arrière-plan** boîte et hello **des notifications à distance** boîte.</span><span class="sxs-lookup"><span data-stu-id="60291-104">Select hello **Enable Background Modes** box and hello **Remote notifications** box.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-22.png)
3. <span data-ttu-id="60291-105">Double-cliquez sur votre projet dans tooopen du Panneau de configuration de Solution hello **Options du projet**.</span><span class="sxs-lookup"><span data-stu-id="60291-105">Double-click your project in hello Solution Panel tooopen **Project Options**.</span></span>
4. <span data-ttu-id="60291-106">Sous **générer**, choisissez **signature d’offre groupée iOS**et sélectionnez hello identité correspondante et profil de configuration vous venez de définir pour ce projet.</span><span class="sxs-lookup"><span data-stu-id="60291-106">Under **Build**, choose **iOS Bundle Signing**, and select hello corresponding identity and provisioning profile you just set up for this project.</span></span>

   ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-20.png)

   <span data-ttu-id="60291-107">Cela garantit que ce projet hello utilise le nouveau profil de hello pour la signature de code.</span><span class="sxs-lookup"><span data-stu-id="60291-107">This ensures that hello project uses hello new profile for code signing.</span></span> <span data-ttu-id="60291-108">Hello officiel Xamarin unité documentation de configuration, consultez [Xamarin configuration].</span><span class="sxs-lookup"><span data-stu-id="60291-108">For hello official Xamarin device provisioning documentation, see [Xamarin Device Provisioning].</span></span>

#### <a name="configure-hello-ios-project-in-visual-studio"></a><span data-ttu-id="60291-109">Configurer le projet d’iOS hello dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="60291-109">Configure hello iOS project in Visual Studio</span></span>
1. <span data-ttu-id="60291-110">Dans Visual Studio, cliquez sur le projet de hello, puis cliquez sur **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="60291-110">In Visual Studio, right-click hello project, and then click **Properties**.</span></span>
2. <span data-ttu-id="60291-111">Dans les pages de propriétés de hello, cliquez sur hello **iOS Application** onglet et mise à jour hello **identificateur** avec l’ID de hello que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="60291-111">In hello properties pages, click hello **iOS Application** tab, and update hello **Identifier** with hello ID that you created earlier.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-23.png)
3. <span data-ttu-id="60291-112">Bonjour **signature d’offre groupée iOS** sous l’onglet identité correspondante de sélection hello et de configuration de profil vous venez de définir pour ce projet.</span><span class="sxs-lookup"><span data-stu-id="60291-112">In hello **iOS Bundle Signing** tab, select hello corresponding identity and provisioning profile you just set up for this project.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-24.png)

    <span data-ttu-id="60291-113">Cela garantit que ce projet hello utilise le nouveau profil de hello pour la signature de code.</span><span class="sxs-lookup"><span data-stu-id="60291-113">This ensures that hello project uses hello new profile for code signing.</span></span> <span data-ttu-id="60291-114">Hello officiel Xamarin unité documentation de configuration, consultez [Xamarin configuration].</span><span class="sxs-lookup"><span data-stu-id="60291-114">For hello official Xamarin device provisioning documentation, see [Xamarin Device Provisioning].</span></span>
4. <span data-ttu-id="60291-115">Double-cliquez sur le fichier Info.plist tooopen, puis activez **RemoteNotifications** sous **Modes d’arrière-plan**.</span><span class="sxs-lookup"><span data-stu-id="60291-115">Double-click Info.plist tooopen it, and then enable **RemoteNotifications** under **Background Modes**.</span></span>

[Xamarin configuration]: http://developer.xamarin.com/guides/ios/getting_started/installation/device_provisioning/
