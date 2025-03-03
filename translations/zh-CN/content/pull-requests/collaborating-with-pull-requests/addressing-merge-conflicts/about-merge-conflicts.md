---
title: 关于合并冲突
intro: 在合并竞争提交的分支时会发生合并冲突，Git 需要您帮助确定最终合并中要加入哪些更改。
redirect_from:
  - /github/collaborating-with-issues-and-pull-requests/addressing-merge-conflicts/about-merge-conflicts
  - /articles/about-merge-conflicts
  - /github/collaborating-with-issues-and-pull-requests/about-merge-conflicts
  - /github/about-merge-conflicts
  - /github/collaborating-with-pull-requests/addressing-merge-conflicts/about-merge-conflicts
versions:
  fpt: '*'
  ghec: '*'
  ghes: '*'
  ghae: '*'
topics:
  - Pull requests
ms.openlocfilehash: 5902f74a9c51772dc3f1d8883b60723ffec3e1d1
ms.sourcegitcommit: 47bd0e48c7dba1dde49baff60bc1eddc91ab10c5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/05/2022
ms.locfileid: '145129653'
---
Git 通常可以自动解决分支之间的冲突并合并它们。 通常，更改发生在不同的行，甚至不同的文件，因此计算机容易理解合并。 但是，有时存在竞争更改的情况，如果没有您的帮助，Git 无法解决。 通常，当人们对相同文件的相同行进行不同的更改时，或者一个人编辑文件而另一个人删除同一文件时，就会发生合并冲突。

您必须解决所有合并冲突后，才能合并 {% data variables.product.product_name %} 上的拉取请求。 如果在拉取请求中的比较分支与基本分支之间存在合并冲突，你可以在“合并拉取请求”按钮上方查看包含冲突更改的文件列表。 “合并拉取请求”按钮在你解决比较分支与基本分支之间的所有冲突之前会一直停用。

![合并冲突错误消息](/assets/images/help/pull_requests/merge_conflict_error_on_github.png)

## 解决合并冲突

要解决合并冲突，必须手动编辑冲突的文件以选择要保留在最终合并中的更改。 解决合并冲突有多种不同的方式：

- 如果合并冲突是竞争行更改而引起的，例如人们对 Git 仓库中不同分支上相同文件的相同行进行不同的更改，您可以使用冲突编辑器在 {% data variables.product.product_name %} 上解决。 有关详细信息，请参阅“[在 {% data variables.product.prodname_dotcom %} 上解决合并冲突](/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/resolving-a-merge-conflict-on-github)”。
- 对于所有其他类型的合并冲突，必须在仓库的本地克隆版本上解决，然后将更改推送到 {% data variables.product.product_name %} 上的分支。 可以使用命令行或 [{% data variables.product.prodname_desktop %}](https://desktop.github.com/) 之类的工具推送更改。 有关详细信息，请参阅“[在命令行上解决合并冲突](/github/collaborating-with-pull-requests/addressing-merge-conflicts/resolving-a-merge-conflict-using-the-command-line)”。

如果您在命令行上有合并冲突，则在计算机本地解决合并冲突之前，无法将本地更改推送到 {% data variables.product.product_name %}。 如果尝试在命令行上合并具有合并冲突的分支，将会收到错误消息。 有关详细信息，请参阅“[使用命令行解决合并冲突](/articles/resolving-a-merge-conflict-using-the-command-line/)”。
```shell
$ git merge <em>BRANCH-NAME</em>
> Auto-merging styleguide.md
> CONFLICT (content): Merge conflict in styleguide.md
> Automatic merge failed; fix conflicts and then commit the result
```

## 延伸阅读

- [关于拉取请求合并](/articles/about-pull-request-merges/)
- [关于拉取请求](/articles/about-pull-requests/)
- [使用命令行解决合并冲突](/github/collaborating-with-pull-requests/addressing-merge-conflicts/resolving-a-merge-conflict-using-the-command-line)
- [在 GitHub 上解决合并冲突](/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/resolving-a-merge-conflict-on-github)
