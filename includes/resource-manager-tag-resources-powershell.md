<span data-ttu-id="3f3ac-101">La version 3.0 du module AzureRm.Resources inclus des modifications importantes par rapport à l’utilisation des balises.</span><span class="sxs-lookup"><span data-stu-id="3f3ac-101">Version 3.0 of the AzureRm.Resources module included significant changes in how you work with tags.</span></span> <span data-ttu-id="3f3ac-102">Avant de poursuivre, vérifiez votre version :</span><span class="sxs-lookup"><span data-stu-id="3f3ac-102">Before you proceed, check your version:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="3f3ac-103">Si vous avez la version 3.0 ou une version ultérieure, les exemples de cette rubrique fonctionnent avec votre environnement.</span><span class="sxs-lookup"><span data-stu-id="3f3ac-103">If your results show version 3.0 or later, the examples in this topic work with your environment.</span></span> <span data-ttu-id="3f3ac-104">Si vous n’avez pas la version 3.0 ou une version ultérieure, vous devez [mettre à jour votre version](/powershell/azureps-cmdlets-docs/) à l’aide de PowerShell Gallery ou de Web Platform Installer avant de consulter cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="3f3ac-104">If you do not have version 3.0 or later, [update your version](/powershell/azureps-cmdlets-docs/) by using PowerShell Gallery or Web Platform Installer before you proceed with this topic.</span></span>

```powershell
Version
-------
3.5.0
```

<span data-ttu-id="3f3ac-105">Pour afficher les balises existantes pour un *groupe de ressources*, utilisez :</span><span class="sxs-lookup"><span data-stu-id="3f3ac-105">To see the existing tags for a *resource group*, use:</span></span>

```powershell
(Get-AzureRmResourceGroup -Name examplegroup).Tags
```

<span data-ttu-id="3f3ac-106">Le script retourne les informations au format suivant :</span><span class="sxs-lookup"><span data-stu-id="3f3ac-106">That script returns the following format:</span></span>

```powershell
Name                           Value
----                           -----
Dept                           IT
Environment                    Test
```

<span data-ttu-id="3f3ac-107">Pour afficher les balises existantes pour une *ressource dont l’ID de ressource est spécifié*, utilisez :</span><span class="sxs-lookup"><span data-stu-id="3f3ac-107">To see the existing tags for a *resource that has a specified resource ID*, use:</span></span>

```powershell
(Get-AzureRmResource -ResourceId {resource-id}).Tags
```

<span data-ttu-id="3f3ac-108">Alternativement, pour afficher les balises existantes pour une *ressource dont le nom et le groupe de ressources sont spécifiés*, utilisez :</span><span class="sxs-lookup"><span data-stu-id="3f3ac-108">Or, to see the existing tags for a *resource that has a specified name and resource group*, use:</span></span>

```powershell
(Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
```

<span data-ttu-id="3f3ac-109">Pour obtenir *les groupes de ressources contenant une balise spécifique*, utilisez :</span><span class="sxs-lookup"><span data-stu-id="3f3ac-109">To get *resource groups that have a specific tag*, use:</span></span>

```powershell
(Find-AzureRmResourceGroup -Tag @{ Dept="Finance" }).Name 
```

<span data-ttu-id="3f3ac-110">Pour obtenir *les ressources contenant une balise spécifique*, utilisez :</span><span class="sxs-lookup"><span data-stu-id="3f3ac-110">To get *resources that have a specific tag*, use:</span></span>

```powershell
(Find-AzureRmResource -TagName Dept -TagValue Finance).Name
```

<span data-ttu-id="3f3ac-111">Chaque fois que vous appliquez des balises à une ressource ou un groupe de ressources, vous remplacez les balises existantes de cette ressource ou de ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="3f3ac-111">Every time you apply tags to a resource or a resource group, you overwrite the existing tags on that resource or resource group.</span></span> <span data-ttu-id="3f3ac-112">Par conséquent, vous devez utiliser une approche différente selon que la ressource ou le groupe de ressources a des balises existantes.</span><span class="sxs-lookup"><span data-stu-id="3f3ac-112">Therefore, you must use a different approach based on whether the resource or resource group has existing tags.</span></span> 

<span data-ttu-id="3f3ac-113">Pour ajouter des balises à un *groupe de ressources ne contenant pas de balises existantes*, utilisez :</span><span class="sxs-lookup"><span data-stu-id="3f3ac-113">To add tags to a *resource group without existing tags*, use:</span></span>

```powershell
Set-AzureRmResourceGroup -Name examplegroup -Tag @{ Dept="IT"; Environment="Test" }
```

<span data-ttu-id="3f3ac-114">Pour ajouter des balises à un *groupe de ressources avec des balises existantes*, récupérez les balises existantes, ajoutez la nouvelle balise et réappliquez les balises :</span><span class="sxs-lookup"><span data-stu-id="3f3ac-114">To add tags to a *resource group that has existing tags*, retrieve the existing tags, add the new tag, and reapply the tags:</span></span>

```powershell
$tags = (Get-AzureRmResourceGroup -Name examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResourceGroup -Tag $tags -Name examplegroup
```

<span data-ttu-id="3f3ac-115">Pour ajouter des balises à une *ressource ne contenant pas de balises existantes*, utilisez :</span><span class="sxs-lookup"><span data-stu-id="3f3ac-115">To add tags to a *resource without existing tags*, use:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName examplevnet -ResourceGroupName examplegroup
```

<span data-ttu-id="3f3ac-116">Pour ajouter des balises à une *ressource avec des balises existantes*, utilisez :</span><span class="sxs-lookup"><span data-stu-id="3f3ac-116">To add tags to a *resource that has existing tags*, use:</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName examplevnet -ResourceGroupName examplegroup
```

<span data-ttu-id="3f3ac-117">Pour appliquer toutes les balises d’un groupe de ressources à ses ressources *sans conserver les balises existantes*, utilisez le script suivant :</span><span class="sxs-lookup"><span data-stu-id="3f3ac-117">To apply all tags from a resource group to its resources, and *not retain existing tags on the resources*, use the following script:</span></span>

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName | ForEach-Object {Set-AzureRmResource -ResourceId $_.ResourceId -Tag $g.Tags -Force } 
}
```

<span data-ttu-id="3f3ac-118">Pour appliquer toutes les balises d’un groupe de ressources à ses ressources et *conserver les balises existantes sur les ressources qui ne sont pas des doublons*, utilisez le script suivant :</span><span class="sxs-lookup"><span data-stu-id="3f3ac-118">To apply all tags from a resource group to its resources, and *retain existing tags on resources that are not duplicates*, use the following script:</span></span>

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    if ($g.Tags -ne $null) {
        $resources = Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName 
        foreach ($r in $resources)
        {
            $resourcetags = (Get-AzureRmResource -ResourceId $r.ResourceId).Tags
            foreach ($key in $g.Tags.Keys)
            {
                if ($resourcetags.ContainsKey($key)) { $resourcetags.Remove($key) }
            }
            $resourcetags += $g.Tags
            Set-AzureRmResource -Tag $resourcetags -ResourceId $r.ResourceId -Force
        }
    }
}
```

<span data-ttu-id="3f3ac-119">Pour supprimer toutes les balises, utilisez une table de hachage vide :</span><span class="sxs-lookup"><span data-stu-id="3f3ac-119">To remove all tags, pass an empty hash table:</span></span>

```powershell
Set-AzureRmResourceGroup -Tag @{} -Name examplegroup
```



