# CLAUDE.md（AWS Cloud Practitioner 対策ツールの引き継ぎメモ）

## 何のリポジトリか
- AWS Certified Cloud Practitioner（CLF-C02、日本語版）の対策ツール。`index.html` 1つで動く（外部ライブラリなし）。
- 公開ページ：https://mitsuhitokawada.github.io/aws-clf-taisaku/（GitHub Pages、main の / から自動で反映。1〜2分）
- 受験日：2026-11-16（月）14:00、テストセンター。※個人の予定はツール本文に書かない（公開ページのため）。受験日は画面で入力し、ブラウザに保存する。
- このリポジトリが元のファイル。mitsu-docs のコピーとアーティファクトは古くなってよい。

## 会話のしかた（ユーザーの好み）
- 関西弁で話す。コード内のコメント・ドキュメントは日本語。
- 略語は正式名を併記する。追加・変更したら、どこに入れたかを毎回言う。作ったファイルはフルパスを最後に表示。
- 確認してから答える。「ありじゃない？」と言われたら、まず自分の説明の間違いを疑う。
- 励ましすぎず、成績の数字を根拠に。合格の保証はしない。
- 公開・送信などの外に出す操作は、確認してから。
- 費用を気にしている。エージェントを大量に回すのは、頼まれたときだけ。

## 学習の回し方
ユーザーが解く → 間違い・迷い・まぐれを、選んだ答えと一緒に文字で貼る → 解剖（正解と合図の言葉、選択肢ごとの判定と理由、間違えた理由の推測、覚え方、見分けのコツ）→ ツールに反映（問題・精読・早見表・用語集・ペア）→ 印をつける → 印つきで再挑戦。

## index.html の仕組み（`<script>` の中のデータ）
- SECTIONS（0=総仕上げ、1〜4=ドメイン。配点 24/30/34/12）、PLAN（受験日から逆算）、READ（精読）、PGROUPS・PRODUCTS（早見表、k:1=★）、TRAPS（TRAP 01〜12）、PAIRS、STUMBLE、TECH、GLOSS、QS（問題）。
- 問題の形：`Q(s,'問題文',['選択肢',...],[正解の添字],'解説HTML','TRAP 06')`。追加分は `QS.push({s,q,o,a,e,trap,src})`（src＝根拠の公式URL。解説の下にリンクが出る）。
- 「/* ==== 追加分（公式資料をもとにエージェントが作成）… ==== */」のブロックは、2026-11-05 に公式ドキュメントから作った190問など。
- 保存（localStorage）：aws_wrong、aws_hist、aws_resume、aws_flag、aws_theme、aws_exam。

## 守ること（コード）
1. 問題は「/* ---- ここより上に問題を追加する」の直前に足す。途中に挿入しない（ID がずれる）。
2. 印（nw:true）は、その下の NW_HEADS に問題文の先頭の文字列を足す。印の処理は問題の追加より後。
3. 解説に選択肢の記号（A・B…）を書かない（選択肢はシャッフルされる）。中身で言い換える。
4. 「2つ選べ」は画面が自動で付けるので、問題文に書かない。選択肢は最大5つ。
5. 問題は本番問題・ダンプ・他サイトの問題を使わない。公式の事実からオリジナルで作る。範囲は公式の試験ガイド（改訂1.3、2026-10-29）で確認。
6. 確認：ブラウザで開いて、全タブの表示、`QS.filter(q=>!q.a.every(i=>i>=0&&i<q.o.length)).length===0`、ID と問題文の重複なし、コンソールのエラーなし、スマホ幅（375px）で `document.documentElement.scrollWidth` が375。
7. Python で文字列を置換するときは、assert で置換対象が1つだけあることを確認する。

## 覚えておく事実（2026年11月時点）
- 試験：65問（採点50＋採点外15）、90分、700/1000で合格。無回答は不正解。
- サポートプラン：Basic（無料）、Business Support+（1アカウント月29ドル〜、24時間の技術サポート、Trusted Advisor 全チェック）、Enterprise Support（月5,000ドル〜、TAM あり）、Unified Operations（月50,000ドル〜）。旧 Developer・Business・Enterprise On-Ramp は 2027-01-01 に終了。
- 試験ガイドの改訂は公開の約1か月後に試験へ反映。旧名と新名の両方を押さえる（QuickSight→Amazon Quick、SageMaker→SageMaker AI など。用語集の「旧名→新名」）。
- ルートユーザーにしかできない作業は、IAM のドキュメントの公式の一覧で確認する（アカウント名・連絡先の変更は IAM でも可）。

## 次にやること
- D1 から精読とクイズ。ユーザーが貼った間違いを解剖して反映する。
- 2026-11-05 に8分野すべての追加問題を入れた（合計324問）。旧名・新名：AppStream 2.0→WorkSpaces Applications、Application Migration Service→AWS Transform MGN。Migration Hub、Application Discovery Service、WorkSpaces Secure Browser は新規受付を終了。
