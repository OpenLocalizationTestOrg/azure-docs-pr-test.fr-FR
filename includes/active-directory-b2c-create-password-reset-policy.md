<span data-ttu-id="0ea97-101">tooenable mot de passe affinées réinitialiser sur votre application, vous devez toocreate une stratégie de réinitialisation de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="0ea97-101">tooenable fine-grained password reset on your application, you will need toocreate a password reset policy.</span></span> <span data-ttu-id="0ea97-102">Notez que ce mot de passe à l’échelle du locataire hello réinitialiser l’option spécifiée [ici](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md).</span><span class="sxs-lookup"><span data-stu-id="0ea97-102">Note that hello tenant-wide password reset option specified [here](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md).</span></span> <span data-ttu-id="0ea97-103">Cette stratégie décrit les expériences hello qui parcourt les consommateurs hello lors de la réinitialisation de mot de passe et le contenu hello de jetons qui hello application recevra de réussite.</span><span class="sxs-lookup"><span data-stu-id="0ea97-103">This policy describes hello experiences that hello consumers will go through during password reset and hello contents of tokens that hello application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="0ea97-104">Dans section de stratégies hello des paramètres, sélectionnez **réinitialise les stratégies de mot de passe** et cliquez sur **+ ajouter**.</span><span class="sxs-lookup"><span data-stu-id="0ea97-104">In hello policies section of settings, select **Password reset policies** and click **+ Add**.</span></span>

![Sélectionner des stratégies d’inscription ou de la connexion et cliquez sur le bouton Ajouter de hello](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-policy.png)

<span data-ttu-id="0ea97-106">Entrez une stratégie **nom** pour tooreference de votre application.</span><span class="sxs-lookup"><span data-stu-id="0ea97-106">Enter a policy **Name** for your application tooreference.</span></span> <span data-ttu-id="0ea97-107">Par exemple, entrez : `SSPR`.</span><span class="sxs-lookup"><span data-stu-id="0ea97-107">For example, enter `SSPR`.</span></span>

<span data-ttu-id="0ea97-108">Cliquez sur **Fournisseurs d’identité** et sélectionnez **Réinitialiser le mot de passe à l’aide de l’adresse e-mail**.</span><span class="sxs-lookup"><span data-stu-id="0ea97-108">Select **Identity providers** and check **Reset password using email address**.</span></span> <span data-ttu-id="0ea97-109">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0ea97-109">Click **OK**.</span></span>

![Sélectionnez la réinitialisation de mot de passe à l’aide d’adresse de messagerie en tant que fournisseur d’identité et cliquez sur hello OK](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-identity-providers.png)

<span data-ttu-id="0ea97-111">Cliquez sur **Revendications de l’application**.</span><span class="sxs-lookup"><span data-stu-id="0ea97-111">Select **Application claims**.</span></span> <span data-ttu-id="0ea97-112">Choisissez les revendications à renvoyer dans les jetons d’autorisation hello envoyées arrière tooyour application après la réinitialisation d’un mot de passe réussie expérience.</span><span class="sxs-lookup"><span data-stu-id="0ea97-112">Choose claims you want returned in hello authorization tokens sent back tooyour application after a successful password reset experience.</span></span> <span data-ttu-id="0ea97-113">Par exemple, sélectionnez **ID d’objet de l’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="0ea97-113">For example, select **User's Object ID**.</span></span>

![Sélectionnez des revendications d’application et cliquez sur le bouton OK](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-application-claims.png)

<span data-ttu-id="0ea97-115">Cliquez sur **créer** stratégie de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="0ea97-115">Click **Create** tooadd hello policy.</span></span> <span data-ttu-id="0ea97-116">stratégie de Hello est répertorié en tant que **B2C_1_SSPR**.</span><span class="sxs-lookup"><span data-stu-id="0ea97-116">hello policy is listed as **B2C_1_SSPR**.</span></span> <span data-ttu-id="0ea97-117">Hello **B2C_1_** préfixe est ajouté toohello nom.</span><span class="sxs-lookup"><span data-stu-id="0ea97-117">hello **B2C_1_** prefix is appended toohello name.</span></span>

<span data-ttu-id="0ea97-118">Ouvrez la stratégie de hello en sélectionnant **B2C_1_SSPR**.</span><span class="sxs-lookup"><span data-stu-id="0ea97-118">Open hello policy by selecting **B2C_1_SSPR**.</span></span> <span data-ttu-id="0ea97-119">Vérifiez les paramètres de hello spécifiés dans la table de hello, puis cliquez sur **exécuter maintenant**.</span><span class="sxs-lookup"><span data-stu-id="0ea97-119">Verify hello settings specified in hello table then click **Run now**.</span></span>

![Sélectionner la stratégie et l’exécuter](media/active-directory-b2c-create-password-reset-policy/run-b2c-password-reset-policy.png)

| <span data-ttu-id="0ea97-121">Paramètre</span><span class="sxs-lookup"><span data-stu-id="0ea97-121">Setting</span></span>      | <span data-ttu-id="0ea97-122">Valeur</span><span class="sxs-lookup"><span data-stu-id="0ea97-122">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="0ea97-123">**Applications**</span><span class="sxs-lookup"><span data-stu-id="0ea97-123">**Applications**</span></span> | <span data-ttu-id="0ea97-124">Application de Contoso B2C</span><span class="sxs-lookup"><span data-stu-id="0ea97-124">Contoso B2C app</span></span> |
| <span data-ttu-id="0ea97-125">**Sélectionner l’URL de réponse**</span><span class="sxs-lookup"><span data-stu-id="0ea97-125">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="0ea97-126">Un nouvel onglet de navigateur s’ouvre et vous pouvez vérifier l’expérience des utilisateurs dans votre application de réinitialisation de mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="0ea97-126">A new browser tab opens, and you can verify hello password reset consumer experience in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="0ea97-127">Il occupe minute tooa pour la création de stratégies et met à jour tootake effet.</span><span class="sxs-lookup"><span data-stu-id="0ea97-127">It takes up tooa minute for policy creation and updates tootake effect.</span></span>
>
