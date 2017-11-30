---
title: "ISymUnmanagedDocument::GetSourceRange 方法"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ISymUnmanagedDocument.GetSourceRange
api_location: diasymreader.dll
api_type: COM
f1_keywords: ISymUnmanagedDocument::GetSourceRange
helpviewer_keywords:
- ISymUnmanagedDocument::GetSourceRange method [.NET Framework debugging]
- GetSourceRange method [.NET Framework debugging]
ms.assetid: 20fefee7-1040-41ba-93dc-bd42f68b90c2
topic_type: apiref
caps.latest.revision: "8"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 6c47f1f491b184e9abe9d56d0729100b0d9b36a7
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2017
---
# <a name="isymunmanageddocumentgetsourcerange-method"></a><span data-ttu-id="680d0-102">ISymUnmanagedDocument::GetSourceRange 方法</span><span class="sxs-lookup"><span data-stu-id="680d0-102">ISymUnmanagedDocument::GetSourceRange Method</span></span>
<span data-ttu-id="680d0-103">返回到给定缓冲区中嵌入源的指定的范围。</span><span class="sxs-lookup"><span data-stu-id="680d0-103">Returns the specified range of the embedded source into the given buffer.</span></span> <span data-ttu-id="680d0-104">缓冲区必须足够大以保存源。</span><span class="sxs-lookup"><span data-stu-id="680d0-104">The buffer must be large enough to hold the source.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="680d0-105">语法</span><span class="sxs-lookup"><span data-stu-id="680d0-105">Syntax</span></span>  
  
```  
HRESULT GetSourceRange(  
    [in]  ULONG32  startLine,  
    [in]  ULONG32  startColumn,  
    [in]  ULONG32  endLine,  
    [in]  ULONG32  endColumn,  
    [in]  ULONG32  cSourceBytes,  
    [out] ULONG32  *pcSourceBytes,  
    [out, size_is(cSourceBytes),  
        length_is(*pcSourceBytes)] BYTE source[]);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="680d0-106">参数</span><span class="sxs-lookup"><span data-stu-id="680d0-106">Parameters</span></span>  
 `startLine`  
 <span data-ttu-id="680d0-107">[in]当前文档中的起始行。</span><span class="sxs-lookup"><span data-stu-id="680d0-107">[in] The starting line in the current document.</span></span>  
  
 `startColumn`  
 <span data-ttu-id="680d0-108">[in]当前文档中的起始列。</span><span class="sxs-lookup"><span data-stu-id="680d0-108">[in] The starting column in the current document.</span></span>  
  
 `endLine`  
 <span data-ttu-id="680d0-109">[in]当前文档中的最后一行。</span><span class="sxs-lookup"><span data-stu-id="680d0-109">[in] The final line in the current document.</span></span>  
  
 `endColumn`  
 <span data-ttu-id="680d0-110">[in]当前文档中最后一列。</span><span class="sxs-lookup"><span data-stu-id="680d0-110">[in] The final column in the current document.</span></span>  
  
 `cSourceBytes`  
 <span data-ttu-id="680d0-111">[in]源，以字节为单位的大小。</span><span class="sxs-lookup"><span data-stu-id="680d0-111">[in] The size of the source, in bytes.</span></span>  
  
 `pcSourceBytes`  
 <span data-ttu-id="680d0-112">[out]指向接收源大小的变量的指针。</span><span class="sxs-lookup"><span data-stu-id="680d0-112">[out] A pointer to a variable that receives the source size.</span></span>  
  
 `source`  
 <span data-ttu-id="680d0-113">[out]大小和源文档，以字节为单位的指定范围的长度。</span><span class="sxs-lookup"><span data-stu-id="680d0-113">[out] The size and length of the specified range of the source document, in bytes.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="680d0-114">返回值</span><span class="sxs-lookup"><span data-stu-id="680d0-114">Return Value</span></span>  
 <span data-ttu-id="680d0-115">如果该方法成功，则为 S_OK。</span><span class="sxs-lookup"><span data-stu-id="680d0-115">S_OK if the method succeeds.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="680d0-116">另请参阅</span><span class="sxs-lookup"><span data-stu-id="680d0-116">See Also</span></span>  
 [<span data-ttu-id="680d0-117">ISymUnmanagedDocument 接口</span><span class="sxs-lookup"><span data-stu-id="680d0-117">ISymUnmanagedDocument Interface</span></span>](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanageddocument-interface.md)