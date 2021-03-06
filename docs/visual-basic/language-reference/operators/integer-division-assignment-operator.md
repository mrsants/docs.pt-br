---
title: Operador \=
ms.date: 07/20/2015
f1_keywords:
- '\='
- vb.\=
helpviewer_keywords:
- '\= operator [Visual Basic]'
- assignment statements [Visual Basic], compound
- statements [Visual Basic], compound assignment
- operator \= [Visual Basic]
- compound assignment statements [Visual Basic]
ms.assetid: 6f39915d-e398-4045-afcc-da6885e57b9c
ms.openlocfilehash: 6e749e13c0427354db9e361538d4bef10b6c6b04
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90873410"
---
# <a name="-operator"></a>\\= Operador

Divide o valor de uma variável ou propriedade pelo valor de uma expressão e atribui o resultado inteiro à variável ou à propriedade.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
variableorproperty \= expression  
```  
  
## <a name="parts"></a>Partes  

 `variableorproperty`  
 Necessário. Qualquer variável numérica ou propriedade.  
  
 `expression`  
 Obrigatórios. Qualquer expressão numérica.  
  
## <a name="remarks"></a>Comentários  

 O elemento no lado esquerdo do `\=` operador pode ser uma variável escalar simples, uma propriedade ou um elemento de uma matriz. A variável ou a propriedade não pode ser [ReadOnly](../modifiers/readonly.md).  
  
 O `\=` operador divide o valor de uma variável ou propriedade à esquerda pelo valor à direita e atribui o resultado inteiro à variável ou à propriedade à sua esquerda  
  
 Para obter mais informações sobre divisão de inteiros, consulte [\ Operator (Visual Basic)](integer-division-operator.md).  
  
## <a name="overloading"></a>Sobrecarga  

 O `\` operador pode ser *sobrecarregado*, o que significa que uma classe ou estrutura pode redefinir seu comportamento quando um operando tem o tipo dessa classe ou estrutura. Sobrecarregar o `\` operador afeta o comportamento do `\=` operador. Se o seu código usa `\=` em uma classe ou estrutura que sobrecarrega, certifique-se de `\` entender seu comportamento redefinido. Para obter mais informações, consulte [procedimentos de operador](../../programming-guide/language-features/procedures/operator-procedures.md).  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir usa o `\=` operador para dividir uma `Integer` variável por um segundo e atribuir o resultado inteiro à primeira variável.  
  
 [!code-vb[VbVbalrOperators#19](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#19)]  
  
## <a name="see-also"></a>Confira também

- [Operador \ (Visual Basic)](integer-division-operator.md)
- [Operador/= (Visual Basic)](floating-point-division-assignment-operator.md)
- [Operadores de atribuição](assignment-operators.md)
- [Operadores aritméticos](arithmetic-operators.md)
- [Precedência do operador no Visual Basic](operator-precedence.md)
- [Operadores Listados por Funcionalidade](operators-listed-by-functionality.md)
- [Instruções](../../programming-guide/language-features/statements.md)
