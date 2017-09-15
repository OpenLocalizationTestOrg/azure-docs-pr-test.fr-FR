<span data-ttu-id="51f8f-101">Pour activer la modification de profil dans votre application, vous devez créer une stratégie de modification de profil.</span><span class="sxs-lookup"><span data-stu-id="51f8f-101">To enable profile editing on your application, you will need to create a profile editing policy.</span></span> <span data-ttu-id="51f8f-102">Cette stratégie décrit les expériences des clients lors de la modification du profil et le contenu des jetons que l'application reçoit en cas d'opération réussie.</span><span class="sxs-lookup"><span data-stu-id="51f8f-102">This policy describes the experiences that consumers will go through during profile editing and the contents of tokens that the application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="51f8f-103">Dans la section stratégie des paramètres, sélectionnez **Stratégies de modification de profil** et cliquez sur **+ Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="51f8f-103">In the policies section of settings, select **Profile editing policies** and click **+ Add**.</span></span>

![Sélectionnez les stratégies de modification de profil et cliquez sur le bouton Ajouter.](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-policy.png)

<span data-ttu-id="51f8f-105">Entrez un **Nom** de stratégie servant de référence pour votre application.</span><span class="sxs-lookup"><span data-stu-id="51f8f-105">Enter a policy **Name** for your application to reference.</span></span> <span data-ttu-id="51f8f-106">Par exemple, entrez : `SiPe`.</span><span class="sxs-lookup"><span data-stu-id="51f8f-106">For example, enter `SiPe`.</span></span>

<span data-ttu-id="51f8f-107">Cliquez sur **Fournisseurs d’identité** et sélectionnez **Connexion du compte local**.</span><span class="sxs-lookup"><span data-stu-id="51f8f-107">Select **Identity providers** and check **Local Account Signin**.</span></span> <span data-ttu-id="51f8f-108">Si vous le souhaitez, vous pouvez également sélectionner des fournisseurs d'identité sociaux, s'ils sont déjà configurés.</span><span class="sxs-lookup"><span data-stu-id="51f8f-108">Optionally, you can also select social identity providers, if already configured.</span></span> <span data-ttu-id="51f8f-109">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="51f8f-109">Click **OK**.</span></span>

![Sélectionnez la Connexion du compte local comme fournisseur d’identité et cliquez sur le bouton OK](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-identity-providers.png)

<span data-ttu-id="51f8f-111">Cliquez sur **Attributs de profil**.</span><span class="sxs-lookup"><span data-stu-id="51f8f-111">Select **Profile attributes**.</span></span> <span data-ttu-id="51f8f-112">Choisissez les attributs que le client peut afficher et modifier sur son profil.</span><span class="sxs-lookup"><span data-stu-id="51f8f-112">Choose attributes the consumer can view and edit in their profile.</span></span> <span data-ttu-id="51f8f-113">Par exemple, vérifiez **Pays/région**, **Nom d’affichage** et **Code postal**.</span><span class="sxs-lookup"><span data-stu-id="51f8f-113">For example, check **Country/Region**, **Display Name**, and **Postal Code**.</span></span> <span data-ttu-id="51f8f-114">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="51f8f-114">Click **OK**.</span></span>

![Sélectionnez certains attributs et cliquez sur le bouton OK](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-attributes.png)

<span data-ttu-id="51f8f-116">Cliquez sur **Revendications de l’application**.</span><span class="sxs-lookup"><span data-stu-id="51f8f-116">Select **Application claims**.</span></span> <span data-ttu-id="51f8f-117">Choisissez les revendications à renvoyer à votre application dans les jetons d’authentification après une expérience de modification de profil réussie.</span><span class="sxs-lookup"><span data-stu-id="51f8f-117">Choose claims you want returned in the authorization tokens sent back to your application after a successful profile editing experience.</span></span> <span data-ttu-id="51f8f-118">Par exemple, sélectionnez **Nom d’affichage** et **Code postal**.</span><span class="sxs-lookup"><span data-stu-id="51f8f-118">For example, select **Display Name**, **Postal Code**.</span></span>

![Sélectionnez des revendications d’application et cliquez sur le bouton OK](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-application-claims.png)

<span data-ttu-id="51f8f-120">Cliquez sur **Créer** pour ajouter la stratégie.</span><span class="sxs-lookup"><span data-stu-id="51f8f-120">Click **Create** to add the policy.</span></span> <span data-ttu-id="51f8f-121">La stratégie est répertoriée en tant que **B2C_1_SiPe**.</span><span class="sxs-lookup"><span data-stu-id="51f8f-121">The policy is listed as **B2C_1_SiPe**.</span></span> <span data-ttu-id="51f8f-122">Le préfixe **B2C_1_** est ajouté au nom.</span><span class="sxs-lookup"><span data-stu-id="51f8f-122">The **B2C_1_** prefix is appended to the name.</span></span>

<span data-ttu-id="51f8f-123">Ouvrez la stratégie en sélectionnant **B2C_1_SiPe**.</span><span class="sxs-lookup"><span data-stu-id="51f8f-123">Open the policy by selecting **B2C_1_SiPe**.</span></span> <span data-ttu-id="51f8f-124">Vérifiez les paramètres spécifiés dans la table, puis cliquez sur **Exécuter maintenant**.</span><span class="sxs-lookup"><span data-stu-id="51f8f-124">Verify the settings specified in the table then click **Run now**.</span></span>

![Sélectionner la stratégie et l’exécuter](media/active-directory-b2c-create-profile-editing-policy/run-b2c-editing-policy.png)

| <span data-ttu-id="51f8f-126">Paramètre</span><span class="sxs-lookup"><span data-stu-id="51f8f-126">Setting</span></span>      | <span data-ttu-id="51f8f-127">Valeur</span><span class="sxs-lookup"><span data-stu-id="51f8f-127">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="51f8f-128">**Applications**</span><span class="sxs-lookup"><span data-stu-id="51f8f-128">**Applications**</span></span> | <span data-ttu-id="51f8f-129">Application de Contoso B2C</span><span class="sxs-lookup"><span data-stu-id="51f8f-129">Contoso B2C app</span></span> |
| <span data-ttu-id="51f8f-130">**Sélectionner l’URL de réponse**</span><span class="sxs-lookup"><span data-stu-id="51f8f-130">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="51f8f-131">Un nouvel onglet de navigateur s’ouvre et vous pouvez vérifier l’expérience du client consistant à modifier un profil telle qu’elle a été configurée.</span><span class="sxs-lookup"><span data-stu-id="51f8f-131">A new browser tab opens, and you can verify the profile editing consumer experience as configured.</span></span>

> [!NOTE]
> <span data-ttu-id="51f8f-132">La création de la stratégie et les mises à jour peuvent prendre jusqu’à une minute.</span><span class="sxs-lookup"><span data-stu-id="51f8f-132">It takes up to a minute for policy creation and updates to take effect.</span></span>
>