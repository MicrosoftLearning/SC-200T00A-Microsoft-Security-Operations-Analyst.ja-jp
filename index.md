---
title: オンラインでホスティングされている手順
permalink: index.html
layout: home
ms.openlocfilehash: 48436bf256577230c0be301c1c30a2ad321ed1ef
ms.sourcegitcommit: 20cbc7b52187d61fca294ac2c00146c2c7c6d337
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2022
ms.locfileid: "137899219"
---
# <a name="content-directory"></a>コンテンツ ディレクトリ

各ラボの演習とデモへのハイパーリンクを以下に示します。

## <a name="labs"></a>ラボ

{% assign labs = site.pages | where_exp:"page", "page.url contains '/Instructions/Labs'" %}
| モジュール | ラボ |
| --- | --- | 
{% for activity in labs %}| {{ activity.lab.module }} | [{{ activity.lab.title }}{% if activity.lab.type %} - {{ activity.lab.type }}{% endif %}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
