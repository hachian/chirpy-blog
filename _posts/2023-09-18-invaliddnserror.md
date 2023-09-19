---
title: GitHub Pagesのカスタムドメイン設定でInvalidDNSErrorが出る
date: 2023-09-17 14:33:50
categories: [tech]
tags: [github, error, github-pages, deploy, domain]
math: false
author: hachian
---

GitHub Pagesのカスタムドメイン設定でエラーが出たときの対処法の備忘録です。

## エラー内容

GitHubのリポジトリから`Settings` → `Pages`と移動し、`Custom domain`という項目でカスタムドメイン設定を行いました。

設定を完了すると、`NotServedByPagesError`や`InvalidDNSError`が出てしまいました。エラーの種類はアクセスするタイミングで異なり、`InvalidDNSError`のほうが多かったです。

エラーは以下の画像のように表示されます。

![Alt text](/assets/img/2023-09-18-snippet/image.png)

## まずは公式ドキュメント

考えられる原因として、設定方法が誤っている可能性があるので、まずは公式ドキュメントを参照することをお勧めします。

- [GitHub Pagesのカスタムドメイン](https://docs.github.com/ja/pages/configuring-a-custom-domain-for-your-github-pages-site/about-custom-domains-and-github-pages)
- [カスタムドメインのトラブルシューティング](https://docs.github.com/ja/pages/configuring-a-custom-domain-for-your-github-pages-site/troubleshooting-custom-domains-and-github-pages#cname-errors)

私は何度も公式ドキュメントを読み返しましたが、エラーの解消までに時間がかかりました。

## 公式ドキュメントに従っている場合

翌日、設定から13時間後に再びアクセスしたところ、エラーは解消していました。

![Alt text](/assets/img/2023-09-18-snippet/image-1.png)

画像下にある`Enforce HTTPS`のチェックボックスも有効になりました。チェックすることで、GitHub Pagesにカスタムドメインを設定し、HTTPSでアクセスるすことができるようになりました。

## 参考リンク

下記のリンクでも、時間を置くようにアドバイスされています。色々調べると、1時間かかるとか15分かかったとか半日かかったとか、人によって解決までにかかる時間はまちまちのようでした。

- [stack overflow](https://stackoverflow.com/questions/54059217/how-to-fix-domain-does-not-resolve-to-the-github-pages-server-error-in-github)
- [GitHub Community](https://github.com/orgs/community/discussions/35168)
