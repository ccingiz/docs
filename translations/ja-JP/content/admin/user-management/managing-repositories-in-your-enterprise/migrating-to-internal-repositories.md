---
title: インターナルリポジトリへの移行
intro: 'インターナルリポジトリへ移行して、{% data variables.product.prodname_ghe_server %}と{% data variables.product.prodname_ghe_cloud %}の両方を使う開発者の内部ソースに関する体験を統合できます。'
redirect_from:
  - /enterprise/admin/installation/migrating-to-internal-repositories
  - /enterprise/admin/user-management/migrating-to-internal-repositories
  - /admin/user-management/migrating-to-internal-repositories
permissions: Site administrators can migrate to internal repositories.
versions:
  ghes: '*'
type: how_to
topics:
  - Enterprise
  - Privacy
  - Repositories
  - Security
shortTitle: Internal repository migration
ms.openlocfilehash: 66a535d8fd2e20cbcc78791588ca2b50ae8ede79
ms.sourcegitcommit: 47bd0e48c7dba1dde49baff60bc1eddc91ab10c5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/05/2022
ms.locfileid: '145116286'
---
## インターナルリポジトリについて

インターナルリポジトリは、{% data variables.product.prodname_ghe_server %} 2.20+で利用できます。 {% data reusables.repositories.about-internal-repos %} 詳細については、「[リポジトリについて](/repositories/creating-and-managing-repositories/about-repositories#about-repository-visibility)」を参照してください。

{% data variables.product.prodname_ghe_server %}の将来のリリースでは、リポジトリの可視性の動作を調整し、パブリック、インターナル、プライベートという用語が{% data variables.product.prodname_ghe_server %}と{% data variables.product.prodname_ghe_cloud %}の開発者に対して統一的な意味合いを持つようにします。

これらの変更に備えるために、もしプライベートモードを有効化しているなら、インスタンスで移行を行ってパブリックリポジトリをインターナルに変換できます。 この移行は現時点ではオプションであり、非プロダクションのインスタンスで変更をテストできるようにするためのものです。 この移行は、将来は必須になります。

移行を行うと、インスタンス上でOrganizationが所有するすべてのパブリックリポジトリは、インターナルリポジトリになります。 それらのリポジトリのいずれかがフォークを持っていれば、そのフォークはプライベートになります。 プライベートリポジトリは、プライベートのままになります。

インスタンス上でユーザアカウントが所有するすべてのパブリックリポジトリは、プライベートリポジトリになります。 それらのリポジトリのいずれかがフォークを持っていれば、そのフォークもプライベートになります。 各フォークの所有者は、フォークの親に対して読み取り権限が与えられます。

インターナルもしくはプライベートになるパブリックリポジトリに対する匿名Git読み取りアクセスは、無効化されます。

リポジトリに対する現在のデフォルトの可視性がパブリックであれば、デフォルトはインターナルになります。 現在のデフォルトがプライベートであれば、デフォルトは変更されません。 デフォルトはいつでも変更できます。 詳細については、「[Enterprise でリポジトリ管理ポリシーを適用する](/admin/policies/enforcing-repository-management-policies-in-your-enterprise#configuring-the-default-visibility-of-new-repositories-in-your-enterprise)」を参照してください。

インスタンスに対するリポジトリの作成ポリシーは、パブリックリポジトリの無効化とプライベート及びインターナルリポジトリの許可に変更されます。 このポリシーはいつでも更新できます。 詳細については、「[インスタンス内でのリポジトリの作成を制限する](/enterprise/admin/user-management/restricting-repository-creation-in-your-instance)」を参照してください。

プライベートモードを有効化していないなら、移行スクリプトは何もしません。

## 移行の実施

1. 管理シェルに接続します。 詳細については、「[管理シェル (SSH) にアクセスする](/enterprise/admin/installation/accessing-the-administrative-shell-ssh)」を参照してください。
{% ifversion ghes or ghae %}
2. 移行コマンドを実行します。

   ```shell
   github-env bin/safe-ruby lib/github/transitions/20191210220630_convert_public_ghes_repos_to_internal.rb --verbose -w |  tee -a /tmp/convert_public_ghes_repos_to_internal.log
   ```

{% else %}
2. `/data/github/current` ディレクトリに移動します。
   ```shell
   cd /data/github/current
   ```
3. 移行コマンドを実行します。
   ```shell
   sudo bin/safe-ruby lib/github/transitions/20191210220630_convert_public_ghes_repos_to_internal.rb --verbose -w | tee -a /tmp/convert_public_ghes_repos_to_internal.log
   ```
{% endif %}

ログ出力がターミナルと `/tmp/convert_public_ghes_repos_to_internal.log` に表示されます。

## 参考資料

- [プライベート モードの有効化](/enterprise/admin/installation/enabling-private-mode)
