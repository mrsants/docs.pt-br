---
title: A avaliação de função está desabilitada porque uma avaliação de função anterior atingiu o tempo limite
ms.date: 07/20/2015
f1_keywords:
- bc30957
- vbc30957
helpviewer_keywords:
- BC30957
ms.assetid: 561e593a-f50a-4b72-a708-4cab60ec7b28
ms.openlocfilehash: 6367553df38a7ccf3b4afbeec877f88fc3d3a1da
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2020
ms.locfileid: "92160679"
---
# <a name="bc30957-function-evaluation-is-disabled-because-a-previous-function-evaluation-timed-out"></a>BC30957: a avaliação de função está desabilitada porque uma avaliação de função anterior atingiu o tempo limite

A avaliação de função está desabilitada porque uma avaliação de função anterior atingiu o tempo limite. Para reabilitar a avaliação da função, execute novamente ou reinicie a depuração.

 No depurador do Visual Studio, uma expressão especifica uma chamada de procedimento, mas outra avaliação atingiu o tempo limite.

 As possíveis causas de uma chamada de procedimento para o tempo limite incluem um loop infinito ou um *loop infinito*. Para obter mais informações, consulte [para... Próxima instrução](../statements/for-next-statement.md).

 Um caso especial de um loop infinito é a *recursão*. Para obter mais informações, consulte [procedimentos recursivos](../../programming-guide/language-features/procedures/recursive-procedures.md).

 **ID do erro:** BC30957

## <a name="to-correct-this-error"></a>Para corrigir este erro

1. Se possível, determine qual foi a avaliação da função anterior e o que causou o tempo limite. Caso contrário, você pode encontrar esse erro novamente.

2. Siga as etapas do depurador novamente ou encerre e reinicie a depuração.

## <a name="see-also"></a>Veja também

- [Depurando no Visual Studio](/visualstudio/debugger/debugger-feature-tour)
- [Navegar pelo Código com o Depurador](/visualstudio/debugger/navigating-through-code-with-the-debugger)
