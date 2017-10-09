<span data-ttu-id="a210a-101">Avec Azure Resource Manager, vous définissez des paramètres pour les valeurs souhaitées toospecify lorsque le modèle de hello est déployé.</span><span class="sxs-lookup"><span data-stu-id="a210a-101">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="a210a-102">modèle de Hello inclut une section appelée paramètres qui contient toutes les valeurs de paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="a210a-102">hello template includes a section called Parameters that contains all of hello parameter values.</span></span>
<span data-ttu-id="a210a-103">Vous devez définir un paramètre pour les valeurs qui varient en fonction de projet que vous déployez hello ou dans l’environnement hello que vous effectuez le déploiement.</span><span class="sxs-lookup"><span data-stu-id="a210a-103">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="a210a-104">Ne définissez pas de paramètres pour les valeurs qui resteront toujours hello même.</span><span class="sxs-lookup"><span data-stu-id="a210a-104">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="a210a-105">Chaque valeur de paramètre est utilisé dans hello modèle toodefine hello ressources qui sont déployés.</span><span class="sxs-lookup"><span data-stu-id="a210a-105">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span> 

<span data-ttu-id="a210a-106">Lorsque vous définissez des paramètres, utilisez hello **allowedValues** toospecify champ dont les valeurs d’un utilisateur peut fournir au cours du déploiement.</span><span class="sxs-lookup"><span data-stu-id="a210a-106">When defining parameters, use hello **allowedValues** field toospecify which values a user can provide during deployment.</span></span> <span data-ttu-id="a210a-107">Hello d’utilisation **defaultValue** champ tooassign un paramètre de toohello value, si aucune valeur n’est fournie au cours du déploiement.</span><span class="sxs-lookup"><span data-stu-id="a210a-107">Use hello **defaultValue** field tooassign a value toohello parameter, if no value is provided during deployment.</span></span>

<span data-ttu-id="a210a-108">Nous allons examiner chaque paramètre dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="a210a-108">We will describe each parameter in hello template.</span></span>

### <a name="sitename"></a><span data-ttu-id="a210a-109">siteName</span><span class="sxs-lookup"><span data-stu-id="a210a-109">siteName</span></span>
<span data-ttu-id="a210a-110">nom de Hello de hello l’application web que vous souhaitez toocreate.</span><span class="sxs-lookup"><span data-stu-id="a210a-110">hello name of hello web app that you wish toocreate.</span></span>

    "siteName":{
      "type":"string"
    }

### <a name="hostingplanname"></a><span data-ttu-id="a210a-111">hostingPlanName</span><span class="sxs-lookup"><span data-stu-id="a210a-111">hostingPlanName</span></span>
<span data-ttu-id="a210a-112">nom Hello Hello du Service d’applications plan toouse pour l’hébergement de l’application web hello.</span><span class="sxs-lookup"><span data-stu-id="a210a-112">hello name of hello App Service plan toouse for hosting hello web app.</span></span>

    "hostingPlanName":{
      "type":"string"
    }

### <a name="sku"></a><span data-ttu-id="a210a-113">sku</span><span class="sxs-lookup"><span data-stu-id="a210a-113">sku</span></span>
<span data-ttu-id="a210a-114">Hello niveau tarifaire pour hello plan d’hébergement.</span><span class="sxs-lookup"><span data-stu-id="a210a-114">hello pricing tier for hello hosting plan.</span></span>

    "sku": {
      "type": "string",
      "allowedValues": [
        "F1",
        "D1",
        "B1",
        "B2",
        "B3",
        "S1",
        "S2",
        "S3",
        "P1",
        "P2",
        "P3",
        "P4"
      ],
      "defaultValue": "S1",
      "metadata": {
        "description": "hello pricing tier for hello hosting plan."
      }
    }

<span data-ttu-id="a210a-115">modèle de Hello définit les valeurs hello qui sont autorisées pour ce paramètre et affecte la valeur par défaut (S1) si aucune valeur n’est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="a210a-115">hello template defines hello values that are permitted for this parameter, and assigns a default value (S1) if no value is specified.</span></span>

### <a name="workersize"></a><span data-ttu-id="a210a-116">workerSize</span><span class="sxs-lookup"><span data-stu-id="a210a-116">workerSize</span></span>
<span data-ttu-id="a210a-117">taille des instances Hello Hello (petite, moyen ou grand) de plan d’hébergement.</span><span class="sxs-lookup"><span data-stu-id="a210a-117">hello instance size of hello hosting plan (small, medium, or large).</span></span>

    "workerSize":{
      "type":"string",
      "allowedValues":[
        "0",
        "1",
        "2"
      ],
      "defaultValue":"0"
    }

<span data-ttu-id="a210a-118">modèle de Hello définit les valeurs hello qui sont autorisées pour ce paramètre (0, 1 ou 2) et affecte la valeur par défaut (0) si aucune valeur n’est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="a210a-118">hello template defines hello values that are permitted for this parameter (0, 1, or 2), and assigns a default value (0) if no value is specified.</span></span> <span data-ttu-id="a210a-119">les valeurs Hello correspondent toosmall, moyenne et grande.</span><span class="sxs-lookup"><span data-stu-id="a210a-119">hello values correspond toosmall, medium and large.</span></span>

