# 第6回 解答

## 演習

<!-- [tool call] の行は、表示された行をそのまま貼り付けてください。終わらなかった STEP は、空欄のままでかまいません。 -->

- STEP 1 のツールの名前：glossary_search_glossary
- STEP 2 の [tool call]：glossary_search_glossary({'query': '3レベル'})
- STEP 3 の [tool call]：fetch_fetch({'url': 'https://modelcontextprotocol.io/'})
- STEP 4 の [tool call]：
  - aws_aws___search_documentation({'search_phrase': 'Amazon S3 バージョニング 概要', 'topics': ['general']})
  - aws_aws___search_documentation({'search_phrase': 'Using versioning Amazon S3 developer guide', 'topics': ['general']})
- 気づき・疑問：3つのサーバーを接続していても、STEP 2 では用語集のツールが呼ばれた。STEP 4 では日本語と英語の検索語で2回検索していた。

## 宿題

<!-- 基礎・実装・発展のどれか1つに取り組めば完了です。 -->

- 取り組んだレベル：基礎
- やったこと：app/mcp_server.py に server.tool()(tools.get_lecture_summary) を1行追加し、「第2回では何を学びますか？」と質問して追加前後を比べた。宿題ではエージェント側の設定とコードは変えていない。
- 結果：
  - 追加前：glossary_search_glossary({'query': '第2回'}) が呼ばれ、用語の定義をもとに LoRA や QLoRA を中心に回答した。
  - 追加後：glossary_get_lecture_summary({'lecture': 2}) が呼ばれ、回のタイトル「ファインチューニングとLoRA」、ねらい、SFT、演習内容を含む回答になった。
  - uv run pytest -q は21件すべて成功した。
- 気づき・疑問：サーバー側でツールを公開するだけで、エージェントが質問に合うツールを呼べた。回の内容を聞く質問では、用語検索より要点を取得するツールの方が全体像をつかみやすかった。
