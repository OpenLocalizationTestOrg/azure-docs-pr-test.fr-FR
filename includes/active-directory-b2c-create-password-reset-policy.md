<span data-ttu-id="2c446-101">Pour activer la réinitialisation affinée du mot de passe sur votre application, vous devez créer une stratégie de réinitialisation du mot de passe.</span><span class="sxs-lookup"><span data-stu-id="2c446-101">To enable fine-grained password reset on your application, you will need to create a password reset policy.</span></span> <span data-ttu-id="2c446-102">Notez que l’option de réinitialisation du mot de passe au niveau du client est spécifiée [ici](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md).</span><span class="sxs-lookup"><span data-stu-id="2c446-102">Note that the tenant-wide password reset option specified [here](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md).</span></span> <span data-ttu-id="2c446-103">Cette stratégie décrit les expériences des clients lors de la réinitialisation du mot de passe et le contenu des jetons que l’application reçoit en cas d’opération réussie.</span><span class="sxs-lookup"><span data-stu-id="2c446-103">This policy describes the experiences that the consumers will go through during password reset and the contents of tokens that the application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="2c446-104">Dans la section stratégie des paramètres, sélectionnez **Stratégies de modification de mot de passe** et cliquez sur **+ Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="2c446-104">In the policies section of settings, select **Password reset policies** and click **+ Add**.</span></span>

![Sélectionnez des stratégies d’inscription ou de connexion et cliquez sur Ajouter.](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-policy.png)

<span data-ttu-id="2c446-106">Entrez un **Nom** de stratégie servant de référence pour votre application.</span><span class="sxs-lookup"><span data-stu-id="2c446-106">Enter a policy **Name** for your application to reference.</span></span> <span data-ttu-id="2c446-107">Par exemple, entrez : `SSPR`.</span><span class="sxs-lookup"><span data-stu-id="2c446-107">For example, enter `SSPR`.</span></span>

<span data-ttu-id="2c446-108">Cliquez sur **Fournisseurs d’identité** et sélectionnez **Réinitialiser le mot de passe à l’aide de l’adresse e-mail**.</span><span class="sxs-lookup"><span data-stu-id="2c446-108">Select **Identity providers** and check **Reset password using email address**.</span></span> <span data-ttu-id="2c446-109">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="2c446-109">Click **OK**.</span></span>

![Sélectionnez la réinitialisation du mot de passe à l’aide de l’adresse e-mail et cliquez sur OK.](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-identity-providers.png)

<span data-ttu-id="2c446-111">Cliquez sur **Revendications de l’application**.</span><span class="sxs-lookup"><span data-stu-id="2c446-111">Select **Application claims**.</span></span> <span data-ttu-id="2c446-112">Choisissez les revendications à renvoyer à votre application dans les jetons d’authentification après une expérience de réinitialisation du mot de passe réussie.</span><span class="sxs-lookup"><span data-stu-id="2c446-112">Choose claims you want returned in the authorization tokens sent back to your application after a successful password reset experience.</span></span> <span data-ttu-id="2c446-113">Par exemple, sélectionnez **ID d’objet de l’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="2c446-113">For example, select **User's Object ID**.</span></span>

![Sélectionnez des revendications d’application et cliquez sur le bouton OK](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-application-claims.png)

<span data-ttu-id="2c446-115">Cliquez sur **Créer** pour ajouter la stratégie.</span><span class="sxs-lookup"><span data-stu-id="2c446-115">Click **Create** to add the policy.</span></span> <span data-ttu-id="2c446-116">La stratégie est répertoriée en tant que **B2C_1_SSPR**.</span><span class="sxs-lookup"><span data-stu-id="2c446-116">The policy is listed as **B2C_1_SSPR**.</span></span> <span data-ttu-id="2c446-117">Le préfixe **B2C_1_** est ajouté au nom.</span><span class="sxs-lookup"><span data-stu-id="2c446-117">The **B2C_1_** prefix is appended to the name.</span></span>

<span data-ttu-id="2c446-118">Ouvrez la stratégie en sélectionnant **B2C_1_SSPR**.</span><span class="sxs-lookup"><span data-stu-id="2c446-118">Open the policy by selecting **B2C_1_SSPR**.</span></span> <span data-ttu-id="2c446-119">Vérifiez les paramètres spécifiés dans la table, puis cliquez sur **Exécuter maintenant**.</span><span class="sxs-lookup"><span data-stu-id="2c446-119">Verify the settings specified in the table then click **Run now**.</span></span>

![Sélectionner la stratégie et l’exécuter](media/active-directory-b2c-create-password-reset-policy/run-b2c-password-reset-policy.png)

| <span data-ttu-id="2c446-121">Paramètre</span><span class="sxs-lookup"><span data-stu-id="2c446-121">Setting</span></span>      | <span data-ttu-id="2c446-122">Valeur</span><span class="sxs-lookup"><span data-stu-id="2c446-122">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="2c446-123">**Applications**</span><span class="sxs-lookup"><span data-stu-id="2c446-123">**Applications**</span></span> | <span data-ttu-id="2c446-124">Application de Contoso B2C</span><span class="sxs-lookup"><span data-stu-id="2c446-124">Contoso B2C app</span></span> |
| <span data-ttu-id="2c446-125">**Sélectionner l’URL de réponse**</span><span class="sxs-lookup"><span data-stu-id="2c446-125">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="2c446-126">Un nouvel onglet de navigateur s’ouvre et vous pouvez vérifier l’expérience du client consistant à réinitialiser un mot de passe dans votre application.</span><span class="sxs-lookup"><span data-stu-id="2c446-126">A new browser tab opens, and you can verify the password reset consumer experience in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="2c446-127">La création de la stratégie et les mises à jour peuvent prendre jusqu’à une minute.</span><span class="sxs-lookup"><span data-stu-id="2c446-127">It takes up to a minute for policy creation and updates to take effect.</span></span>
>
