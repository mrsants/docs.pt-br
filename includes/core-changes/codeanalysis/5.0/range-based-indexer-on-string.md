---
ms.openlocfilehash: 87f9cc03f334233ef286abd11e6f5ff82d7988c2
ms.sourcegitcommit: 9c45035b781caebc63ec8ecf912dc83fb6723b1f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88811335"
---
### <a name="ca1831-use-asspan-or-asmemory-instead-of-range-based-indexer"></a><span data-ttu-id="8269c-101">CA1831 usar asspan ou asmemory em vez de indexador baseado em intervalo</span><span class="sxs-lookup"><span data-stu-id="8269c-101">CA1831 Use AsSpan or AsMemory instead of Range-based indexer</span></span>

<span data-ttu-id="8269c-102">A regra do analisador de código .NET [CA1831](/visualstudio/code-quality/ca1831) está habilitada, por padrão, a partir do .NET 5,0.</span><span class="sxs-lookup"><span data-stu-id="8269c-102">.NET code analyzer rule [CA1831](/visualstudio/code-quality/ca1831) is enabled, by default, starting in .NET 5.0.</span></span> <span data-ttu-id="8269c-103">Ele produz um aviso de compilação para qualquer código em que um <xref:System.Range> indexador baseado em um é usado em uma cadeia de caracteres, mas nenhuma cópia foi pretendida.</span><span class="sxs-lookup"><span data-stu-id="8269c-103">It produces a build warning for any code where a <xref:System.Range>-based indexer is used on a string, but no copy was intended.</span></span>

#### <a name="change-description"></a><span data-ttu-id="8269c-104">Descrição da alteração</span><span class="sxs-lookup"><span data-stu-id="8269c-104">Change description</span></span>

<span data-ttu-id="8269c-105">A partir do .NET 5,0, o SDK do .NET inclui [analisadores de código-fonte .net](../../../../docs/fundamentals/productivity/code-analysis.md).</span><span class="sxs-lookup"><span data-stu-id="8269c-105">Starting in .NET 5.0, the .NET SDK includes [.NET source code analyzers](../../../../docs/fundamentals/productivity/code-analysis.md).</span></span> <span data-ttu-id="8269c-106">Várias dessas regras estão habilitadas, por padrão, incluindo [CA1831](/visualstudio/code-quality/ca1831).</span><span class="sxs-lookup"><span data-stu-id="8269c-106">Several of these rules are enabled, by default, including [CA1831](/visualstudio/code-quality/ca1831).</span></span> <span data-ttu-id="8269c-107">Se o seu projeto contiver código que viole essa regra e estiver configurado para tratar avisos como erros, essa alteração poderá interromper sua compilação.</span><span class="sxs-lookup"><span data-stu-id="8269c-107">If your project contains code that violates this rule and is configured to treat warnings as errors, this change could break your build.</span></span>

<span data-ttu-id="8269c-108">A regra CA1831 localiza instâncias em que o <xref:System.Range> indexador baseado em um é usado em uma cadeia de caracteres, mas nenhuma cópia foi pretendida.</span><span class="sxs-lookup"><span data-stu-id="8269c-108">Rule CA1831 finds instances where a <xref:System.Range>-based indexer is used on a string, but no copy was intended.</span></span> <span data-ttu-id="8269c-109">Se o <xref:System.Range> indexador baseado for usado diretamente em uma cadeia de caracteres para produzir uma conversão implícita, uma cópia desnecessária da parte solicitada da cadeia de caracteres será criada.</span><span class="sxs-lookup"><span data-stu-id="8269c-109">If the <xref:System.Range>-based indexer is used directly on a string to produce an implicit cast, then an unnecessary copy of the requested portion of the string is created.</span></span> <span data-ttu-id="8269c-110">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="8269c-110">For example:</span></span>

```csharp
ReadOnlySpan<char> slice = str[1..3];
```

<span data-ttu-id="8269c-111">O CA1831 sugere o uso do <xref:System.Range> indexador baseado em um *intervalo* da cadeia de caracteres, em vez disso.</span><span class="sxs-lookup"><span data-stu-id="8269c-111">CA1831 suggests using the <xref:System.Range>-based indexer on a *span* of the string, instead.</span></span> <span data-ttu-id="8269c-112">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="8269c-112">For example:</span></span>

```csharp
ReadOnlySpan<char> slice = str.AsSpan()[1..3];
```

#### <a name="version-introduced"></a><span data-ttu-id="8269c-113">Versão introduzida</span><span class="sxs-lookup"><span data-stu-id="8269c-113">Version introduced</span></span>

<span data-ttu-id="8269c-114">5,0 Preview 8</span><span class="sxs-lookup"><span data-stu-id="8269c-114">5.0 Preview 8</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="8269c-115">Ação recomendada</span><span class="sxs-lookup"><span data-stu-id="8269c-115">Recommended action</span></span>

- <span data-ttu-id="8269c-116">Para corrigir seu código e evitar alocações desnecessárias, chame <xref:System.MemoryExtensions.AsSpan(System.String)> ou <xref:System.MemoryExtensions.AsMemory(System.String)> antes de usar o <xref:System.Range> indexador baseado em.</span><span class="sxs-lookup"><span data-stu-id="8269c-116">To correct your code and avoid unnecessary allocations, call <xref:System.MemoryExtensions.AsSpan(System.String)> or <xref:System.MemoryExtensions.AsMemory(System.String)> before using the <xref:System.Range>-based indexer.</span></span> <span data-ttu-id="8269c-117">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="8269c-117">For example:</span></span>

  ```csharp
  ReadOnlySpan<char> slice = str.AsSpan()[1..3];
  ```

- <span data-ttu-id="8269c-118">Se você não quiser alterar seu código, poderá desabilitar a regra definindo sua severidade como `suggestion` ou `none` .</span><span class="sxs-lookup"><span data-stu-id="8269c-118">If you don't want to change your code, you can disable the rule by setting its severity to `suggestion` or `none`.</span></span> <span data-ttu-id="8269c-119">Para obter mais informações, consulte [configurar regras de análise de código](../../../../docs/fundamentals/productivity/configure-code-analysis-rules.md).</span><span class="sxs-lookup"><span data-stu-id="8269c-119">For more information, see [Configure code analysis rules](../../../../docs/fundamentals/productivity/configure-code-analysis-rules.md).</span></span>

- <span data-ttu-id="8269c-120">Para desabilitar completamente a análise de código, defina `EnableNETAnalyzers` como `false` em seu arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="8269c-120">To disable code analysis completely, set `EnableNETAnalyzers` to `false` in your project file.</span></span> <span data-ttu-id="8269c-121">Para obter mais informações, consulte [EnableNETAnalyzers](../../../../docs/core/project-sdk/msbuild-props.md#enablenetanalyzers).</span><span class="sxs-lookup"><span data-stu-id="8269c-121">For more information, see [EnableNETAnalyzers](../../../../docs/core/project-sdk/msbuild-props.md#enablenetanalyzers).</span></span>

#### <a name="category"></a><span data-ttu-id="8269c-122">Categoria</span><span class="sxs-lookup"><span data-stu-id="8269c-122">Category</span></span>

<span data-ttu-id="8269c-123">Análise de código</span><span class="sxs-lookup"><span data-stu-id="8269c-123">Code analysis</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="8269c-124">APIs afetadas</span><span class="sxs-lookup"><span data-stu-id="8269c-124">Affected APIs</span></span>

- <xref:System.Range?displayProperty=fullName>

<!--

#### Affected APIs

- `T:System.Range`

-->