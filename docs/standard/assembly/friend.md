---
title: Assemblies amigáveis
ms.date: 08/20/2019
ms.assetid: b65ea7de-0801-477a-a39c-e914c2cc107c
dev_langs:
- csharp
- vb
ms.openlocfilehash: 6387e93bcd4efeec57ada9228dcaf015d053dbf7
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70973232"
---
# <a name="friend-assemblies"></a><span data-ttu-id="3824c-102">Assemblies amigáveis</span><span class="sxs-lookup"><span data-stu-id="3824c-102">Friend assemblies</span></span>

<span data-ttu-id="3824c-103">Um *assembly Friend* é um assembly que pode acessar os tipos e membros [internos](../../csharp/language-reference/keywords/internal.md) C#() ou [Friend](../../visual-basic/language-reference/modifiers/friend.md) (Visual Basic) de outro assembly.</span><span class="sxs-lookup"><span data-stu-id="3824c-103">A *friend assembly* is an assembly that can access another assembly's [internal](../../csharp/language-reference/keywords/internal.md) (C#) or [Friend](../../visual-basic/language-reference/modifiers/friend.md) (Visual Basic) types and members.</span></span> <span data-ttu-id="3824c-104">Se você identificar um assembly como um assembly amigável, não precisará marcar os tipos e membros como públicos para que eles sejam acessados por outros assemblies.</span><span class="sxs-lookup"><span data-stu-id="3824c-104">If you identify an assembly as a friend assembly, you no longer have to mark types and members as public in order for them to be accessed by other assemblies.</span></span> <span data-ttu-id="3824c-105">Isso é especialmente conveniente nos seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="3824c-105">This is especially convenient in the following scenarios:</span></span>

- <span data-ttu-id="3824c-106">Durante os testes de unidade, quando o código de teste é executado em um assembly separado, mas exige acesso aos membros do assembly sendo testado que são marcados como `internal` no C# ou `Friend` no Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="3824c-106">During unit testing, when test code runs in a separate assembly but requires access to members in the assembly being tested that are marked as `internal` in C# or `Friend` in Visual Basic.</span></span>

- <span data-ttu-id="3824c-107">Quando você está desenvolvendo uma biblioteca de classes e as adições à biblioteca estão contidas em assemblies separados, mas exigem acesso a membros em assemblies existentes que são marcados como `internal` no C# ou `Friend` no Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="3824c-107">When you are developing a class library and additions to the library are contained in separate assemblies but require access to members in existing assemblies that are marked as `internal` in C# or `Friend` in Visual Basic.</span></span>

## <a name="remarks"></a><span data-ttu-id="3824c-108">Comentários</span><span class="sxs-lookup"><span data-stu-id="3824c-108">Remarks</span></span>

<span data-ttu-id="3824c-109">Você pode usar o atributo <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> para identificar um ou mais assemblies amigáveis para um determinado assembly.</span><span class="sxs-lookup"><span data-stu-id="3824c-109">You can use the <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> attribute to identify one or more friend assemblies for a given assembly.</span></span> <span data-ttu-id="3824c-110">O exemplo a seguir usa <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> o atributo no *assembly A* e especifica o assembly *AssemblyB* como um assembly Friend.</span><span class="sxs-lookup"><span data-stu-id="3824c-110">The following example uses the <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> attribute in *Assembly A* and specifies assembly *AssemblyB* as a friend assembly.</span></span> <span data-ttu-id="3824c-111">Isso dá ao assembly *AssemblyB* acesso a todos os tipos e membros no *assembly A* que são `internal` marcados como `Friend` in C# ou in Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="3824c-111">This gives assembly *AssemblyB* access to all types and members in *Assembly A* that are marked as `internal` in C# or `Friend` in Visual Basic.</span></span>

> [!NOTE]
> <span data-ttu-id="3824c-112">Quando você compila um assembly como *AssemblyB* que acessará tipos internos ou membros internos de outro assembly, como *assembly A*, você deve especificar explicitamente o nome do arquivo de saída ( *. exe* ou *. dll*) usando **/out** opção do compilador.</span><span class="sxs-lookup"><span data-stu-id="3824c-112">When you compile an assembly like *AssemblyB* that will access internal types or internal members of another assembly like *Assembly A*, you must explicitly specify the name of the output file (*.exe* or *.dll*) by using the **/out** compiler option.</span></span> <span data-ttu-id="3824c-113">Isso é necessário porque o compilador ainda não gerou o nome do assembly que está compilando no momento em que ele está se associando às referências externas.</span><span class="sxs-lookup"><span data-stu-id="3824c-113">This is required because the compiler has not yet generated the name for the assembly it is building at the time it is binding to external references.</span></span> <span data-ttu-id="3824c-114">Para obter mais informações, confira [/out (C#)](../../csharp/language-reference/compiler-options/out-compiler-option.md) ou [/out (Visual Basic)](../../visual-basic/reference/command-line-compiler/out.md).</span><span class="sxs-lookup"><span data-stu-id="3824c-114">For more information, see [/out (C#)](../../csharp/language-reference/compiler-options/out-compiler-option.md) or [/out (Visual Basic)](../../visual-basic/reference/command-line-compiler/out.md).</span></span>

```csharp
using System.Runtime.CompilerServices;
using System;

[assembly: InternalsVisibleTo("AssemblyB")]

// The class is internal by default.
class FriendClass
{
    public void Test()
    {
        Console.WriteLine("Sample Class");
    }
}

// Public class that has an internal method.
public class ClassWithFriendMethod
{
    internal void Test()
    {
        Console.WriteLine("Sample Method");
    }

}
```

```vb
Imports System.Runtime.CompilerServices
Imports System
<Assembly: InternalsVisibleTo("AssemblyB")>

' Friend class.
Friend Class FriendClass
    Public Sub Test()
        Console.WriteLine("Sample Class")
    End Sub
End Class

' Public class with a Friend method.
Public Class ClassWithFriendMethod
    Friend Sub Test()
        Console.WriteLine("Sample Method")
    End Sub
End Class
```

<span data-ttu-id="3824c-115">Somente os assemblies que você especifica explicitamente como amigos podem `internal` acessarC#() `Friend` ou (Visual Basic) tipos e membros.</span><span class="sxs-lookup"><span data-stu-id="3824c-115">Only assemblies that you explicitly specify as friends can access `internal` (C#) or `Friend` (Visual Basic) types and members.</span></span> <span data-ttu-id="3824c-116">Por exemplo, se *AssemblyB* for um amigo do *assembly a e o* *assembly c* fizer referência a *AssemblyB*, o *assembly c* não `internal` teráC#acesso aos `Friend` tipos () ou (Visual Basic) no *assembly a* .</span><span class="sxs-lookup"><span data-stu-id="3824c-116">For example, if *AssemblyB* is a friend of *Assembly A* and *Assembly C* references *AssemblyB*, *Assembly C* does not have access to `internal` (C#) or `Friend` (Visual Basic) types in *Assembly A*.</span></span>

<span data-ttu-id="3824c-117">O compilador executa algumas validações básicas do nome do assembly amigável passado para o atributo <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>.</span><span class="sxs-lookup"><span data-stu-id="3824c-117">The compiler performs some basic validation of the friend assembly name passed to the <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> attribute.</span></span> <span data-ttu-id="3824c-118">Se o *assembly A* declarar *AssemblyB* como um assembly Friend, as regras de validação serão as seguintes:</span><span class="sxs-lookup"><span data-stu-id="3824c-118">If *Assembly A* declares *AssemblyB* as a friend assembly, the validation rules are as follows:</span></span>

- <span data-ttu-id="3824c-119">Se *o assembly A tiver um* nome forte, *AssemblyB* também deverá ter um nome forte.</span><span class="sxs-lookup"><span data-stu-id="3824c-119">If *Assembly A* is strong named, *AssemblyB* must also be strong named.</span></span> <span data-ttu-id="3824c-120">O nome do assembly Friend que é passado para o atributo deve consistir no nome do assembly e na chave pública da chave de nome forte que é usada para assinar *AssemblyB*.</span><span class="sxs-lookup"><span data-stu-id="3824c-120">The friend assembly name that is passed to the attribute must consist of the assembly name and the public key of the strong-name key that is used to sign *AssemblyB*.</span></span>

     <span data-ttu-id="3824c-121">O nome do assembly Friend que é passado para <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> o atributo não pode ser o nome forte de *AssemblyB*.</span><span class="sxs-lookup"><span data-stu-id="3824c-121">The friend assembly name that is passed to the <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> attribute cannot be the strong name of *AssemblyB*.</span></span> <span data-ttu-id="3824c-122">Não inclua a versão do assembly, a cultura, a arquitetura ou o token de chave pública.</span><span class="sxs-lookup"><span data-stu-id="3824c-122">Don't include the assembly version, culture, architecture, or public key token.</span></span>

- <span data-ttu-id="3824c-123">Se o *assembly A* não for de nome forte, o nome do assembly Friend deverá consistir apenas no nome do assembly.</span><span class="sxs-lookup"><span data-stu-id="3824c-123">If *Assembly A* is not strong named, the friend assembly name should consist of only the assembly name.</span></span> <span data-ttu-id="3824c-124">Para obter mais informações, confira [Como: Crie assemblies](create-unsigned-friend.md)Friend não assinados.</span><span class="sxs-lookup"><span data-stu-id="3824c-124">For more information, see [How to: Create unsigned friend assemblies](create-unsigned-friend.md).</span></span>

- <span data-ttu-id="3824c-125">Se *AssemblyB* for de nome forte, você deverá especificar a chave de nome forte para *AssemblyB* usando a configuração do projeto ou a opção do `/keyfile` compilador de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="3824c-125">If *AssemblyB* is strong named, you must specify the strong-name key for *AssemblyB* by using the project setting or the command-line `/keyfile` compiler option.</span></span> <span data-ttu-id="3824c-126">Para obter mais informações, confira [Como: Criar assemblies](create-signed-friend.md)Friend assinados.</span><span class="sxs-lookup"><span data-stu-id="3824c-126">For more information, see [How to: Create signed friend assemblies](create-signed-friend.md).</span></span>

 <span data-ttu-id="3824c-127">A classe <xref:System.Security.Permissions.StrongNameIdentityPermission> também fornece a capacidade de compartilhar tipos, com as seguintes diferenças:</span><span class="sxs-lookup"><span data-stu-id="3824c-127">The <xref:System.Security.Permissions.StrongNameIdentityPermission> class also provides the ability to share types, with the following differences:</span></span>

- <span data-ttu-id="3824c-128"><xref:System.Security.Permissions.StrongNameIdentityPermission> aplica-se a um tipo individual, enquanto um assembly amigável se aplica ao assembly inteiro.</span><span class="sxs-lookup"><span data-stu-id="3824c-128"><xref:System.Security.Permissions.StrongNameIdentityPermission> applies to an individual type, while a friend assembly applies to the whole assembly.</span></span>

- <span data-ttu-id="3824c-129">Se houver centenas de tipos no *assembly a* que você deseja compartilhar com *AssemblyB*, você precisará adicionar <xref:System.Security.Permissions.StrongNameIdentityPermission> a todos eles.</span><span class="sxs-lookup"><span data-stu-id="3824c-129">If there are hundreds of types in *Assembly A* that you want to share with *AssemblyB*, you have to add <xref:System.Security.Permissions.StrongNameIdentityPermission> to all of them.</span></span> <span data-ttu-id="3824c-130">Se usar um assembly amigável, você precisará declarar a relação de amigo uma vez.</span><span class="sxs-lookup"><span data-stu-id="3824c-130">If you use a friend assembly, you only need to declare the friend relationship once.</span></span>

- <span data-ttu-id="3824c-131">Se você usar <xref:System.Security.Permissions.StrongNameIdentityPermission>, os tipos que você desejar compartilhar precisarão ser declarados como públicos.</span><span class="sxs-lookup"><span data-stu-id="3824c-131">If you use <xref:System.Security.Permissions.StrongNameIdentityPermission>, the types you want to share have to be declared as public.</span></span> <span data-ttu-id="3824c-132">Se você usar um assembly Friend, os tipos compartilhados serão `internal` declaradosC#como () ou `Friend` (Visual Basic).</span><span class="sxs-lookup"><span data-stu-id="3824c-132">If you use a friend assembly, the shared types are declared as `internal` (C#) or `Friend` (Visual Basic).</span></span>

<span data-ttu-id="3824c-133">Para obter informações sobre como acessar os tipos e `internal` métodosC#de um `Friend` assembly () ou (Visual Basic) de um arquivo de módulo (um arquivo com a extensão *. netmodule* ), consulte [/moduleassemblynameC#()](../../csharp/language-reference/compiler-options/moduleassemblyname-compiler-option.md) ou [/ moduleassemblyname (Visual Basic)](../../visual-basic/reference/command-line-compiler/moduleassemblyname.md).</span><span class="sxs-lookup"><span data-stu-id="3824c-133">For information about how to access an assembly's `internal` (C#) or `Friend` (Visual Basic) types and methods from a module file (a file with the *.netmodule* extension), see [/moduleassemblyname (C#)](../../csharp/language-reference/compiler-options/moduleassemblyname-compiler-option.md) or [/moduleassemblyname (Visual Basic)](../../visual-basic/reference/command-line-compiler/moduleassemblyname.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="3824c-134">Consulte também</span><span class="sxs-lookup"><span data-stu-id="3824c-134">See also</span></span>

- <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>
- <xref:System.Security.Permissions.StrongNameIdentityPermission>
- [<span data-ttu-id="3824c-135">Como: Criar assemblies Friend não assinados</span><span class="sxs-lookup"><span data-stu-id="3824c-135">How to: Create unsigned friend assemblies</span></span>](create-unsigned-friend.md)
- [<span data-ttu-id="3824c-136">Como: Criar assemblies Friend assinados</span><span class="sxs-lookup"><span data-stu-id="3824c-136">How to: Create signed friend assemblies</span></span>](create-signed-friend.md)
- [<span data-ttu-id="3824c-137">Assemblies no .NET</span><span class="sxs-lookup"><span data-stu-id="3824c-137">Assemblies in .NET</span></span>](index.md)
- [<span data-ttu-id="3824c-138">Guia de programação em C#</span><span class="sxs-lookup"><span data-stu-id="3824c-138">C# programming guide</span></span>](../../csharp/programming-guide/index.md)
- [<span data-ttu-id="3824c-139">Conceitos de programação (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="3824c-139">Programming concepts (Visual Basic)</span></span>](../../visual-basic/programming-guide/concepts/index.md)