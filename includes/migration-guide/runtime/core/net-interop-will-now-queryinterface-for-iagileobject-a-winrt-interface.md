---
ms.openlocfilehash: 5b3f9bcb56d3e34568afd8b97fb9ebe09a677f4c
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67802640"
---
### <a name="net-interop-will-now-queryinterface-for-iagileobject-a-winrt-interface"></a><span data-ttu-id="97fb9-101">A Interoperabilidade do .NET agora fará QueryInterface para IAgileObject (uma interface do WinRT)</span><span class="sxs-lookup"><span data-stu-id="97fb9-101">.NET Interop will now QueryInterface for IAgileObject (a WinRT interface)</span></span>

|   |   |
|---|---|
|<span data-ttu-id="97fb9-102">Detalhes</span><span class="sxs-lookup"><span data-stu-id="97fb9-102">Details</span></span>|<span data-ttu-id="97fb9-103">Ao usar um evento de WinRT com um delegado do .NET, Windows fará QI para IAgileObject começando com o .NET Framework 4.8.</span><span class="sxs-lookup"><span data-stu-id="97fb9-103">When using a WinRT event with a .NET delegate, Windows will QI for IAgileObject starting with the .NET Framework 4.8.</span></span>  <span data-ttu-id="97fb9-104">Nas versões anteriores do .NET Framework, o tempo de execução falharia nessa QI e o evento não poderia ser assinado.</span><span class="sxs-lookup"><span data-stu-id="97fb9-104">In previous versions of the .NET Framework, the runtime would fail that QI, and the event could not be subscribed.</span></span><ul><li><span data-ttu-id="97fb9-105">[x] Quirked</span><span class="sxs-lookup"><span data-stu-id="97fb9-105">[ x ] Quirked</span></span></li></ul>|
|<span data-ttu-id="97fb9-106">Sugestão</span><span class="sxs-lookup"><span data-stu-id="97fb9-106">Suggestion</span></span>|<span data-ttu-id="97fb9-107">Se a habilitação de QI para IAgileObject interromper a execução, você poderá desabilitar esse código definindo a configuração a seguir.</span><span class="sxs-lookup"><span data-stu-id="97fb9-107">If enabling the QI for IAgileObject breaks execution, you can disable this code by setting the following configuration.</span></span> <h4><span data-ttu-id="97fb9-108">Método 1: Variável de ambiente</span><span class="sxs-lookup"><span data-stu-id="97fb9-108">Method 1: Environment variable</span></span></h4> <span data-ttu-id="97fb9-109">Defina a variável de ambiente a seguir:COMPLUS_DisableCCWSupportIAgileObject=1Esse método afeta qualquer ambiente que herda essa variável de ambiente.</span><span class="sxs-lookup"><span data-stu-id="97fb9-109">Set the following environment variable:COMPLUS_DisableCCWSupportIAgileObject=1This method affects any environment that inherits this environment variable.</span></span> <span data-ttu-id="97fb9-110">Isso poderá ser apenas uma única sessão de console ou poderá afetar todo o computador se você definir a variável de ambiente globalmente. O nome da variável de ambiente não diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="97fb9-110">This might be just a single console session, or it might affect the entire machine if you set the environment variable globally.The environment variable name is not case-sensitive.</span></span> <h4><span data-ttu-id="97fb9-111">Método 2: Registro</span><span class="sxs-lookup"><span data-stu-id="97fb9-111">Method 2: Registry</span></span></h4> <span data-ttu-id="97fb9-112">Usando o Editor do Registro (regedit.exe), localize qualquer uma das seguintes subchaves:HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft.NETFramework HKEY_CURRENT_USER\SOFTWARE\Microsoft.NETFrameworkEm seguida, adicione o seguinte:Nome do valor: DisableCCWSupportIAgileObject Tipo: DWORD (32 bits) Valor (também chamado REG_WORD) Valor: 1É possível usar a ferramenta REG.EXE do Windows para adicionar esse valor de uma linha de comando ou ambiente de script.</span><span class="sxs-lookup"><span data-stu-id="97fb9-112">Using Registry Editor (regedit.exe), find either of the following subkeys:HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft.NETFramework HKEY_CURRENT_USER\SOFTWARE\Microsoft.NETFrameworkThen add the following:Value name: DisableCCWSupportIAgileObject Type: DWORD (32-bit) Value (also called REG_WORD) Value: 1You can use the Windows REG.EXE tool to add this value from a command-line or scripting environment.</span></span> <span data-ttu-id="97fb9-113">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="97fb9-113">For example:</span></span><pre><code class="lang-console">reg add HKLM\SOFTWARE\Microsoft\.NETFramework /v DisableCCWSupportIAgileObject /t REG_DWORD /d 1&#13;&#10;</code></pre><span data-ttu-id="97fb9-114">Nesse caso, <code>HKLM</code> é usado em vez de <code>HKEY_LOCAL_MACHINE</code>.</span><span class="sxs-lookup"><span data-stu-id="97fb9-114">In this case, <code>HKLM</code> is used instead of <code>HKEY_LOCAL_MACHINE</code>.</span></span> <span data-ttu-id="97fb9-115">Use <code>reg add /?</code> para ver a ajuda sobre essa sintaxe. O nome do valor do Registro não diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="97fb9-115">Use <code>reg add /?</code> to see help on this syntax.The registry value name is not case-sensitive.</span></span>|
|<span data-ttu-id="97fb9-116">Escopo</span><span class="sxs-lookup"><span data-stu-id="97fb9-116">Scope</span></span>|<span data-ttu-id="97fb9-117">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="97fb9-117">Edge</span></span>|
|<span data-ttu-id="97fb9-118">Versão</span><span class="sxs-lookup"><span data-stu-id="97fb9-118">Version</span></span>|<span data-ttu-id="97fb9-119">4.8</span><span class="sxs-lookup"><span data-stu-id="97fb9-119">4.8</span></span>|
|<span data-ttu-id="97fb9-120">Tipo</span><span class="sxs-lookup"><span data-stu-id="97fb9-120">Type</span></span>|<span data-ttu-id="97fb9-121">Tempo de execução</span><span class="sxs-lookup"><span data-stu-id="97fb9-121">Runtime</span></span>|
