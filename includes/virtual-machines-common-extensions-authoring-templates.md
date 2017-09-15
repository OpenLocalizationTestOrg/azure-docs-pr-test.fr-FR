## <a name="overview-of-azure-resource-manager-templates"></a><span data-ttu-id="3cb64-101">Vue d’ensemble des modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3cb64-101">Overview of Azure Resource Manager templates</span></span>
<span data-ttu-id="3cb64-102">Le modèle Azure Resource Manager vous permet de spécifier de manière déclarative l’infrastructure IaaS Azure dans le langage Json en définissant les dépendances entre ressources.</span><span class="sxs-lookup"><span data-stu-id="3cb64-102">Azure Resource Manager templates allow you to declaratively specify the Azure IaaS infrastructure in Json language by defining the dependencies between resources.</span></span> <span data-ttu-id="3cb64-103">Pour obtenir une présentation détaillée des modèles Azure Resource Manager, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="3cb64-103">For a detailed overview of Azure Resource Manager Templates, please refer to the article below:</span></span>

[<span data-ttu-id="3cb64-104">Présentation du groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="3cb64-104">Resource Group Overview</span></span>](../articles/azure-resource-manager/resource-group-overview.md)

## <a name="sample-template-snippet-for-vm-extensions"></a><span data-ttu-id="3cb64-105">Extrait de l’exemple de modèle pour les extensions de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3cb64-105">Sample template snippet for VM extensions</span></span>
<span data-ttu-id="3cb64-106">Pour déployer une extension de machine virtuelle dans le cadre du modèle Azure Resource Manager, vous devez spécifier la configuration de l’extension de façon déclarative dans le modèle.</span><span class="sxs-lookup"><span data-stu-id="3cb64-106">Deploying VM extensions as part of an Azure Resource Manager template requires you to declaratively specify the extension configuration in the template.</span></span>
<span data-ttu-id="3cb64-107">Voici le format qui permet de spécifier la configuration de l’extension.</span><span class="sxs-lookup"><span data-stu-id="3cb64-107">Here is the format for specifying the extension configuration.</span></span>

      {
      "type": "Microsoft.Compute/virtualMachines/extensions",
      "name": "MyExtension",
      "apiVersion": "2015-05-01-preview",
      "location": "[parameters('location')]",
      "dependsOn": ["[concat('Microsoft.Compute/virtualMachines/',parameters('vmName'))]"],
      "properties":
      {
      "publisher": "Publisher Namespace",
      "type": "extension Name",
      "typeHandlerVersion": "extension version",
      "settings": {
      // Extension specific configuration goes in here.
      }
      }
      }

<span data-ttu-id="3cb64-108">Comme vous pouvez le voir ci-dessus, le modèle d’extension contient deux parties principales :</span><span class="sxs-lookup"><span data-stu-id="3cb64-108">As you can see from the above, the extension template contains two main parts:</span></span>

1. <span data-ttu-id="3cb64-109">Nom de l’extension, éditeur et version.</span><span class="sxs-lookup"><span data-stu-id="3cb64-109">Extension name, publisher and version</span></span>
2. <span data-ttu-id="3cb64-110">Configuration de l’extension.</span><span class="sxs-lookup"><span data-stu-id="3cb64-110">Extension Configuration.</span></span>

## <a name="identifying-the-publisher-type-and-typehandlerversion-for-any-extension"></a><span data-ttu-id="3cb64-111">Identification de l’éditeur, du type et de typeHandlerVersion pour les extensions.</span><span class="sxs-lookup"><span data-stu-id="3cb64-111">Identifying the publisher, type, and typeHandlerVersion for any extension</span></span>
<span data-ttu-id="3cb64-112">Les extensions de machine virtuelle Azure sont publiées par Microsoft et approuvées par des éditeurs tiers, et chaque extension est identifiée de façon univoque par son éditeur, son type et la typeHandlerVersion.</span><span class="sxs-lookup"><span data-stu-id="3cb64-112">Azure VM extensions are published by Microsoft and trusted 3rd party publishers and each extension is uniquely identified by its publisher,type and the typeHandlerVersion.</span></span> <span data-ttu-id="3cb64-113">Ils peuvent être déterminés comme suit :</span><span class="sxs-lookup"><span data-stu-id="3cb64-113">These can be determined as following:</span></span>  

