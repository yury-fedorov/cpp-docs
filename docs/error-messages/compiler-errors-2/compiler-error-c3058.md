---
title: "Compiler Error C3058 | Microsoft Docs"
ms.custom: ""
ms.date: "11/04/2016"
ms.reviewer: ""
ms.suite: ""
ms.technology:  
  - "cpp-tools"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "C3058"
dev_langs: 
  - "C++"
helpviewer_keywords: 
  - "C3058"
ms.assetid: 669d08c8-0b58-4351-88aa-c6e6e1af481c
caps.latest.revision: 6
author: "corob-msft"
ms.author: "corob"
manager: "ghogen"
translation.priority.ht: 
  - "de-de"
  - "es-es"
  - "fr-fr"
  - "it-it"
  - "ja-jp"
  - "ko-kr"
  - "ru-ru"
  - "zh-cn"
  - "zh-tw"
translation.priority.mt: 
  - "cs-cz"
  - "pl-pl"
  - "pt-br"
  - "tr-tr"
---
# Compiler Error C3058
'symbol' : symbol not declared as 'threadprivate' before it is used in the 'copyin' clause  
  
 A symbol must first be declared [threadprivate](../../parallel/openmp/reference/threadprivate.md) before it can be used in a [copyin](../../parallel/openmp/reference/copyin.md) clause.  
  
 The following sample generates C3058:  
  
```  
// C3058.cpp  
// compile with: /openmp  
int x, y, z;  
#pragma omp threadprivate(x, z)  
  
void test() {  
   #pragma omp parallel copyin(x, y)   // C3058  
   {  
   }  
}  
```  
  
 Possible resolution:  
  
```  
// C3058b.cpp  
// compile with: /openmp /LD  
int x, y, z;  
#pragma omp threadprivate(x, y)  
  
void test() {  
   #pragma omp parallel copyin(x, y)  
   {  
   }  
}  
```