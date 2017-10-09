<span data-ttu-id="9dae4-101">profil de tooenable modification sur votre application, vous devez toocreate un stratégie de modification du profil.</span><span class="sxs-lookup"><span data-stu-id="9dae4-101">tooenable profile editing on your application, you will need toocreate a profile editing policy.</span></span> <span data-ttu-id="9dae4-102">Cette stratégie décrit les expériences hello qui parcourt les consommateurs pendant contenu hello et de modification du profil de jetons application hello recevra de réussite.</span><span class="sxs-lookup"><span data-stu-id="9dae4-102">This policy describes hello experiences that consumers will go through during profile editing and hello contents of tokens that hello application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="9dae4-103">Dans section de stratégies hello des paramètres, sélectionnez **modification des stratégies de profil** et cliquez sur **+ ajouter**.</span><span class="sxs-lookup"><span data-stu-id="9dae4-103">In hello policies section of settings, select **Profile editing policies** and click **+ Add**.</span></span>

![Sélectionnez les stratégies de modification de profil et cliquez sur le bouton Ajouter de hello](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-policy.png)

<span data-ttu-id="9dae4-105">Entrez une stratégie **nom** pour tooreference de votre application.</span><span class="sxs-lookup"><span data-stu-id="9dae4-105">Enter a policy **Name** for your application tooreference.</span></span> <span data-ttu-id="9dae4-106">Par exemple, entrez : `SiPe`.</span><span class="sxs-lookup"><span data-stu-id="9dae4-106">For example, enter `SiPe`.</span></span>

<span data-ttu-id="9dae4-107">Cliquez sur **Fournisseurs d’identité** et sélectionnez **Connexion du compte local**.</span><span class="sxs-lookup"><span data-stu-id="9dae4-107">Select **Identity providers** and check **Local Account Signin**.</span></span> <span data-ttu-id="9dae4-108">Si vous le souhaitez, vous pouvez également sélectionner des fournisseurs d'identité sociaux, s'ils sont déjà configurés.</span><span class="sxs-lookup"><span data-stu-id="9dae4-108">Optionally, you can also select social identity providers, if already configured.</span></span> <span data-ttu-id="9dae4-109">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="9dae4-109">Click **OK**.</span></span>

![Sélectionnez la connexion de compte Local comme fournisseur d’identité et cliquez sur hello OK](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-identity-providers.png)

<span data-ttu-id="9dae4-111">Cliquez sur **Attributs de profil**.</span><span class="sxs-lookup"><span data-stu-id="9dae4-111">Select **Profile attributes**.</span></span> <span data-ttu-id="9dae4-112">Choisissez le consommateur de hello attributs peut afficher et modifier leur profil.</span><span class="sxs-lookup"><span data-stu-id="9dae4-112">Choose attributes hello consumer can view and edit in their profile.</span></span> <span data-ttu-id="9dae4-113">Par exemple, vérifiez **Pays/région**, **Nom d’affichage** et **Code postal**.</span><span class="sxs-lookup"><span data-stu-id="9dae4-113">For example, check **Country/Region**, **Display Name**, and **Postal Code**.</span></span> <span data-ttu-id="9dae4-114">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="9dae4-114">Click **OK**.</span></span>

![Sélectionnez certains attributs et cliquez sur le bouton de hello OK](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-attributes.png)

<span data-ttu-id="9dae4-116">Cliquez sur **Revendications de l’application**.</span><span class="sxs-lookup"><span data-stu-id="9dae4-116">Select **Application claims**.</span></span> <span data-ttu-id="9dae4-117">Choisissez les revendications à renvoyer dans les jetons d’autorisation hello envoyées application tooyour précédent après une expérience de modification de profil réussie.</span><span class="sxs-lookup"><span data-stu-id="9dae4-117">Choose claims you want returned in hello authorization tokens sent back tooyour application after a successful profile editing experience.</span></span> <span data-ttu-id="9dae4-118">Par exemple, sélectionnez **Nom d’affichage** et **Code postal**.</span><span class="sxs-lookup"><span data-stu-id="9dae4-118">For example, select **Display Name**, **Postal Code**.</span></span>

![Sélectionnez des revendications d’application et cliquez sur le bouton OK](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-application-claims.png)

<span data-ttu-id="9dae4-120">Cliquez sur **créer** stratégie de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="9dae4-120">Click **Create** tooadd hello policy.</span></span> <span data-ttu-id="9dae4-121">stratégie de Hello est répertorié en tant que **B2C_1_SiPe**.</span><span class="sxs-lookup"><span data-stu-id="9dae4-121">hello policy is listed as **B2C_1_SiPe**.</span></span> <span data-ttu-id="9dae4-122">Hello **B2C_1_** préfixe est ajouté toohello nom.</span><span class="sxs-lookup"><span data-stu-id="9dae4-122">hello **B2C_1_** prefix is appended toohello name.</span></span>

<span data-ttu-id="9dae4-123">Ouvrez la stratégie de hello en sélectionnant **B2C_1_SiPe**.</span><span class="sxs-lookup"><span data-stu-id="9dae4-123">Open hello policy by selecting **B2C_1_SiPe**.</span></span> <span data-ttu-id="9dae4-124">Vérifiez les paramètres de hello spécifiés dans la table de hello, puis cliquez sur **exécuter maintenant**.</span><span class="sxs-lookup"><span data-stu-id="9dae4-124">Verify hello settings specified in hello table then click **Run now**.</span></span>

![Sélectionner la stratégie et l’exécuter](media/active-directory-b2c-create-profile-editing-policy/run-b2c-editing-policy.png)

| <span data-ttu-id="9dae4-126">Paramètre</span><span class="sxs-lookup"><span data-stu-id="9dae4-126">Setting</span></span>      | <span data-ttu-id="9dae4-127">Valeur</span><span class="sxs-lookup"><span data-stu-id="9dae4-127">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="9dae4-128">**Applications**</span><span class="sxs-lookup"><span data-stu-id="9dae4-128">**Applications**</span></span> | <span data-ttu-id="9dae4-129">Application de Contoso B2C</span><span class="sxs-lookup"><span data-stu-id="9dae4-129">Contoso B2C app</span></span> |
| <span data-ttu-id="9dae4-130">**Sélectionner l’URL de réponse**</span><span class="sxs-lookup"><span data-stu-id="9dae4-130">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="9dae4-131">Un nouvel onglet de navigateur s’ouvre et vous pouvez vérifier le profil de hello édition consommateur tel que configuré.</span><span class="sxs-lookup"><span data-stu-id="9dae4-131">A new browser tab opens, and you can verify hello profile editing consumer experience as configured.</span></span>

> [!NOTE]
> <span data-ttu-id="9dae4-132">Il occupe minute tooa pour la création de stratégies et met à jour tootake effet.</span><span class="sxs-lookup"><span data-stu-id="9dae4-132">It takes up tooa minute for policy creation and updates tootake effect.</span></span>
>