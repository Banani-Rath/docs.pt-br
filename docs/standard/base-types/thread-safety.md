---
title: "Acesso thread-safe em expressões regulares"
description: "Acesso thread-safe em expressões regulares"
keywords: .NET, .NET Core
author: stevehoag
manager: wpickett
ms.date: 07/28/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: dc64b681-b3aa-4911-8e30-0764a8b6a852
translationtype: Human Translation
ms.sourcegitcommit: fb00da6505c9edb6a49d2003ae9bcb8e74c11d6c
ms.openlocfilehash: ab71ad5ff9148f00f392fddd3c89acbcab874015

---

# <a name="thread-safety-in-regular-expressions"></a>Acesso thread-safe em expressões regulares

A própria classe [Regex](xref:System.Text.RegularExpressions.Regex) é thread-safe e imutável (somente leitura). Ou seja, os objetos de [Regex](xref:System.Text.RegularExpressions.Regex) podem ser criados em qualquer thread e compartilhados entre os threads. Métodos correspondentes podem ser chamados de qualquer thread e nunca alteram nenhum estado global.

No entanto, os objetos de resultado ([Match](xref:System.Text.RegularExpressions.Match) e [MatchCollection)](xref:System.Text.RegularExpressions.MatchCollection) retornados pela [Regex](xref:System.Text.RegularExpressions.Regex) devem ser usados em um único thread. Embora muitos desses objetos sejam logicamente imutáveis, suas implementações poderiam atrasar a computação de alguns resultados para melhorar o desempenho e, como resultado, os chamadores devem serializar o acesso a eles.

Se houver a necessidade de compartilhar os objetos de resultado da [Regex](xref:System.Text.RegularExpressions.Regex) em vários threads, esses objetos poderão ser convertidos em instâncias thread-safe chamando seus métodos sincronizados. Com exceção dos enumeradores, todas as classes de expressões regulares são thread-safe ou podem ser convertidas em objetos thread-safe por um método sincronizado.

Os enumeradores são a única exceção. Um aplicativo precisa serializar as chamadas a enumeradores de coleções. A regra é que se uma coleção pode ser enumerada em mais de um thread simultaneamente, você deve sincronizar os métodos do enumerador no objeto raiz da coleção percorrida pelo enumerador.

## <a name="see-also"></a>Consulte também

[Expressões regulares do .NET](regular-expressions.md)




<!--HONumber=Nov16_HO4-->


