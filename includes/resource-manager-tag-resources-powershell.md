<span data-ttu-id="88889-101">La version 3.0 de module de AzureRm.Resources hello inclus des modifications importantes dans l’utilisation de balises.</span><span class="sxs-lookup"><span data-stu-id="88889-101">Version 3.0 of hello AzureRm.Resources module included significant changes in how you work with tags.</span></span> <span data-ttu-id="88889-102">Avant de poursuivre, vérifiez votre version :</span><span class="sxs-lookup"><span data-stu-id="88889-102">Before you proceed, check your version:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="88889-103">Si les résultats indiquent la version 3.0 ou version ultérieure, les exemples de hello dans cette rubrique fonctionnent avec votre environnement.</span><span class="sxs-lookup"><span data-stu-id="88889-103">If your results show version 3.0 or later, hello examples in this topic work with your environment.</span></span> <span data-ttu-id="88889-104">Si vous n’avez pas la version 3.0 ou une version ultérieure, vous devez [mettre à jour votre version](/powershell/azureps-cmdlets-docs/) à l’aide de PowerShell Gallery ou de Web Platform Installer avant de consulter cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="88889-104">If you do not have version 3.0 or later, [update your version](/powershell/azureps-cmdlets-docs/) by using PowerShell Gallery or Web Platform Installer before you proceed with this topic.</span></span>

```powershell
Version
-------
3.5.0
```

<span data-ttu-id="88889-105">toosee hello balises existantes pour un *groupe de ressources*, utilisez :</span><span class="sxs-lookup"><span data-stu-id="88889-105">toosee hello existing tags for a *resource group*, use:</span></span>

```powershell
(Get-AzureRmResourceGroup -Name examplegroup).Tags
```

<span data-ttu-id="88889-106">Ce script renvoie hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="88889-106">That script returns hello following format:</span></span>

```powershell
Name                           Value
----                           -----
Dept                           IT
Environment                    Test
```

<span data-ttu-id="88889-107">toosee hello balises existantes pour un *ressource qui comporte un ID de ressource spécifié*, utilisez :</span><span class="sxs-lookup"><span data-stu-id="88889-107">toosee hello existing tags for a *resource that has a specified resource ID*, use:</span></span>

```powershell
(Get-AzureRmResource -ResourceId {resource-id}).Tags
```

<span data-ttu-id="88889-108">Ou, toosee hello balises existantes pour un *ressource qui comporte un groupe de ressources et de nom spécifié*, utilisez :</span><span class="sxs-lookup"><span data-stu-id="88889-108">Or, toosee hello existing tags for a *resource that has a specified name and resource group*, use:</span></span>

```powershell
(Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
```

<span data-ttu-id="88889-109">tooget *des groupes de ressources qui ont une balise spécifique*, utilisez :</span><span class="sxs-lookup"><span data-stu-id="88889-109">tooget *resource groups that have a specific tag*, use:</span></span>

```powershell
(Find-AzureRmResourceGroup -Tag @{ Dept="Finance" }).Name 
```

<span data-ttu-id="88889-110">tooget *ressources qui ont une balise spécifique*, utilisez :</span><span class="sxs-lookup"><span data-stu-id="88889-110">tooget *resources that have a specific tag*, use:</span></span>

```powershell
(Find-AzureRmResource -TagName Dept -TagValue Finance).Name
```

<span data-ttu-id="88889-111">Chaque fois que vous appliquez des balises tooa ressource ou un groupe de ressources, vous remplacez les balises existantes hello sur cette ressource ou un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="88889-111">Every time you apply tags tooa resource or a resource group, you overwrite hello existing tags on that resource or resource group.</span></span> <span data-ttu-id="88889-112">Par conséquent, vous devez utiliser une approche différente selon que hello ressource ou un groupe de ressources a des balises existantes.</span><span class="sxs-lookup"><span data-stu-id="88889-112">Therefore, you must use a different approach based on whether hello resource or resource group has existing tags.</span></span> 

<span data-ttu-id="88889-113">tooadd balises tooa *groupe de ressources sans balises existantes*, utilisez :</span><span class="sxs-lookup"><span data-stu-id="88889-113">tooadd tags tooa *resource group without existing tags*, use:</span></span>

```powershell
Set-AzureRmResourceGroup -Name examplegroup -Tag @{ Dept="IT"; Environment="Test" }
```

<span data-ttu-id="88889-114">tooadd balises tooa *groupe de ressources qui comporte des balises existantes*, récupérer les balises existantes hello, ajoutez la balise hello et réappliquer les balises hello :</span><span class="sxs-lookup"><span data-stu-id="88889-114">tooadd tags tooa *resource group that has existing tags*, retrieve hello existing tags, add hello new tag, and reapply hello tags:</span></span>

```powershell
$tags = (Get-AzureRmResourceGroup -Name examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResourceGroup -Tag $tags -Name examplegroup
```

<span data-ttu-id="88889-115">tooadd balises tooa *ressource sans balises existantes*, utilisez :</span><span class="sxs-lookup"><span data-stu-id="88889-115">tooadd tags tooa *resource without existing tags*, use:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName examplevnet -ResourceGroupName examplegroup
```

<span data-ttu-id="88889-116">tooadd balises tooa *ressource qui comporte les balises existantes*, utilisez :</span><span class="sxs-lookup"><span data-stu-id="88889-116">tooadd tags tooa *resource that has existing tags*, use:</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName examplevnet -ResourceGroupName examplegroup
```

<span data-ttu-id="88889-117">tooapply toutes les balises à partir d’un groupe tooits ressources, et *ne conserve pas les balises existantes sur des ressources hello*, utilisez hello script suivant :</span><span class="sxs-lookup"><span data-stu-id="88889-117">tooapply all tags from a resource group tooits resources, and *not retain existing tags on hello resources*, use hello following script:</span></span>

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName | ForEach-Object {Set-AzureRmResource -ResourceId $_.ResourceId -Tag $g.Tags -Force } 
}
```

<span data-ttu-id="88889-118">tooapply toutes les balises à partir d’un groupe tooits ressources, et *conserver les balises existantes sur les ressources qui ne sont pas des doublons*, utilisez hello script suivant :</span><span class="sxs-lookup"><span data-stu-id="88889-118">tooapply all tags from a resource group tooits resources, and *retain existing tags on resources that are not duplicates*, use hello following script:</span></span>

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

<span data-ttu-id="88889-119">tooremove toutes les balises, passez à une table de hachage vide :</span><span class="sxs-lookup"><span data-stu-id="88889-119">tooremove all tags, pass an empty hash table:</span></span>

```powershell
Set-AzureRmResourceGroup -Tag @{} -Name examplegroup
```



