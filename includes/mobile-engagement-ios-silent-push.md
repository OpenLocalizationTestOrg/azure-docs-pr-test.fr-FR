> [!IMPORTANT]
> <span data-ttu-id="a4cc6-101">tooreceive des Notifications Push à partir de Mobile Engagement, vous devez tooenable `Silent Remote Notifications` dans votre application.</span><span class="sxs-lookup"><span data-stu-id="a4cc6-101">tooreceive Push Notifications from Mobile Engagement, you need tooenable `Silent Remote Notifications` in your application.</span></span> <span data-ttu-id="a4cc6-102">Vous devez le tableau UIBackgroundModes toohello tooadd hello valeur de la notification à distance dans votre fichier Info.plist.</span><span class="sxs-lookup"><span data-stu-id="a4cc6-102">You need tooadd hello remote-notification value toohello UIBackgroundModes array in your Info.plist file.</span></span>
> 
> 

1. <span data-ttu-id="a4cc6-103">Ouvrez `info.plist` fichier hello projet</span><span class="sxs-lookup"><span data-stu-id="a4cc6-103">Open `info.plist` file in hello project</span></span>
2. <span data-ttu-id="a4cc6-104">Cliquez avec le bouton droit sur l’élément du haut dans la liste de hello hello (`Information Property List`) et ajouter une nouvelle ligne</span><span class="sxs-lookup"><span data-stu-id="a4cc6-104">Right click on hello top item in hello list (`Information Property List`) and add a new row</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push1.png)
3. <span data-ttu-id="a4cc6-105">Bonjour Entrez nouvelle ligne`Required background modes`</span><span class="sxs-lookup"><span data-stu-id="a4cc6-105">In hello new row enter `Required background modes`</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push2.png)
4. <span data-ttu-id="a4cc6-106">Cliquez sur la ligne de hello tooexpand hello flèche gauche</span><span class="sxs-lookup"><span data-stu-id="a4cc6-106">Click on hello left arrow tooexpand hello row</span></span>
5. <span data-ttu-id="a4cc6-107">Ajouter hello valeur toohello élément 0`App downloads content in response toopush notifications`</span><span class="sxs-lookup"><span data-stu-id="a4cc6-107">Add hello following value toohello item 0 `App downloads content in response toopush notifications`</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push3.png)
6. <span data-ttu-id="a4cc6-108">Une fois que vous modifiez hello, info.plist hello XML doit contenir hello suivant clé et la valeur :</span><span class="sxs-lookup"><span data-stu-id="a4cc6-108">Once you make hello change, hello info.plist XML should contain hello following key and value:</span></span>
   
        <key>UIBackgroundModes</key>
        <array>
        <string>remote-notification</string>
        </array>
7. <span data-ttu-id="a4cc6-109">Si vous utilisez **Xcode 7+** et **iOS 9 +** :</span><span class="sxs-lookup"><span data-stu-id="a4cc6-109">If you are using **Xcode 7+** and **iOS 9+**:</span></span>
   
   * <span data-ttu-id="a4cc6-110">Activer **Notifications Push** dans Cibles > Nom de cible > Fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="a4cc6-110">Enable **Push Notifications** in Targets > Your Target Name > Capabilities.</span></span>

