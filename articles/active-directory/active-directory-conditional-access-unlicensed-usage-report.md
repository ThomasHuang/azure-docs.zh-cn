---
title: "未授权用户使用情况报表 | Microsoft Docs"
description: "未授权用户使用情况报表可帮助你识别正在使用付费 Azure AD 功能的未授权用户。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: mtillman
ms.assetid: 92138f43-9528-4c8a-b834-66a47da476e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/17/2017
ms.author: markvi
ms.openlocfilehash: 298102fedc766d362d1b3c525293212825eef5c7
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2017
---
# <a name="unlicensed-usage-report"></a>未授权用户使用情况报表
未授权用户使用情况报表可帮助你识别正在使用付费 Azure AD 功能的未授权用户。 这样可以更好地使用已购买的许可证，并且让你知道何时可能需要其他许可证。 

该报表显示最近 30 天付费功能的有效使用情况。 

## <a name="report-structure"></a>报表结构
| 列名称 | 说明 |
|:--- |:--- |
| 未授权用户 |用户的名称 |
| 功能 |功能名称。 例如：条件性访问 |
| 访问的应用程序 |通过功能访问的应用程序的名称。 例如：Office 365 SharePoint Online |

> [!NOTE]
> 如果已删除用户帐户，则使用 ID 填充“未授权用户”列，如 1003000090D8B285
> 
> 

## <a name="conditional-access-feature"></a>条件性访问功能
如果未授权用户没有 Azure AD Premium 许可证，那么当他们访问已应用条件性访问策略的服务时，将对他们进行标记。 

这种情况也适用于 MFA / 位置策略和使用 Intune 的设备策略。

## <a name="see-also"></a>另请参阅
* [在 Office 365 和其他连接到 Azure Active Directory 的应用中使用条件性访问](active-directory-conditional-access-azure-portal.md)
* [Azure AD 的条件性访问入门](active-directory-conditional-access-azure-portal-get-started.md) 

