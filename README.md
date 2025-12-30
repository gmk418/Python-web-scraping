# Python Web Scraping Guide

[![Promo](https://github.com/luminati-io/LinkedIn-Scraper/blob/main/Proxies%20and%20scrapers%20GitHub%20bonus%20banner.png)](https://brightdata.jp/products/web-scraper) 

このPython Webスクレイピング用リポジトリでは、Webスクレイピングを始めるために必要なものがすべて見つかります。Webスクレイピングの仕組みを確認し、Pythonにおけるさまざまなアプローチを深掘りし、最後に完全な例をレビューします。

Pythonは、シンプルな構文と豊富なオープンソースライブラリの選択肢により、[Webスクレイピングに最適な言語の1つ](https://brightdata.jp/blog/web-data/best-languages-web-scraping)として広く評価されています。より詳しく学んでいきましょう！

## Table of Contents
- [Web Scraping Logic in Python](#web-scraping-logic-in-python)
- [Python Web Scraping Libraries](#python-web-scraping-libraries)
   * [HTTP Clients](#http-clients)
   * [HTML Parsers](#html-parsers)
   * [Browser Automation](#browser-automation)
   * [All-in-One Scraping](#all-in-one-scraping)
- [Common Stacks for Scraping in Python](#common-stacks-for-scraping-in-python)
- [Prerequisites](#prerequisites)
- [Web Scraping with Requests and Beautiful Soup](#web-scraping-with-requests-and-beautiful-soup)
   * [Features](#features)
      + [Requests](#requests)
      + [Beautiful Soup](#beautiful-soup)
   * [Setup](#setup)
   * [Methods](#methods)
      + [Connect to a Web Page](#connect-to-a-web-page)
      + [Parse an HTML String](#parse-an-html-string)
      + [Basic Node Selection and Data Extraction Methods](#basic-node-selection-and-data-extraction-methods)
      + [Find Nodes](#find-nodes)
      + [Select Nodes](#select-nodes)
- [Export the Scraped Data](#export-the-scraped-data)
   * [CSV Export](#csv-export)
   * [JSON Export](#json-export)
- [Web Scraping Examples in Python](#web-scraping-examples-in-python)
   * [1. Requests + Beautiful Soup](#1-requests-beautiful-soup)
   * [2. Selenium](#2-selenium)
   * [Scrapy](#scrapy)
- [Challenges of Python Web Scraping](#challenges-of-python-web-scraping)
- [Simplified Web Scraping With Web Scraper API](#simplified-web-scraping-with-web-scraper-api)

## Web Scraping Logic in Python
あらゆる[PythonによるWebスクレイピング](https://brightdata.jp/blog/how-tos/web-scraping-with-python)スクリプトの主要な構成要素は次のとおりです：
1. 対象ページのHTMLを取得します。
2. HTMLをPythonオブジェクトにパースします。
3. パースしたHTMLからデータを抽出します。
4. 抽出したデータをCSVやJSONなど、人間が読みやすい形式にエクスポートします。

最初の2ステップのアプローチは、対象ページが静的か動的かによって異なります：
- **静的サイト**：[Requests](https://requests.readthedocs.io/en/latest/)のようなHTTPクライアントを使用して、サーバーから直接HTMLをリクエストします。レスポンスを受け取ったら、[Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)のようなHTMLパーサーでHTMLをパースします。
- **動的サイト**：[Selenium](https://selenium-python.readthedocs.io/)などのブラウザ自動化ツールを使用し、ヘッドレスブラウザでページを読み込みます。このアプローチにより、動的コンテンツをレンダリングしてからブラウザエンジンでパースできます。

ステップ3については、データ抽出の高レベルなロジックはページのDOM構造に依存します。ただし、実装は選択したツールと、それらが提供するHTMLノード選択およびデータ抽出の方法によって変わります。

最後に、[Scrapy](https://scrapy.org/)のようなオールインワンのWebスクレイピングツールもある点に留意してください。これらのライブラリは4つのステップすべてを単一のプラットフォームに統合することでプロセスを簡素化し、スクレイピングのワークフローを効率化します。

## Python Web Scraping Libraries
PythonでのWebスクレイピングに役立つ代表的なライブラリをご紹介します。包括的な一覧については、[Awesome Web Scraping repository](https://github.com/luminati-io/Awesome-Web-Scraping/blob/main/python.md)をご参照ください。

### HTTP Clients
- [`requests`](https://github.com/kennethreitz/requests): シンプルでありながら洗練されたHTTPライブラリです。
- [`httpx`](https://github.com/encode/httpx): Python向けの次世代HTTPクライアントです。
- [`aiohttp`](https://github.com/aio-libs/aiohttp): `asyncio`とPython向けの非同期HTTPクライアント/サーバーフレームワークです。

### HTML Parsers
- [`beautifulsoup4`](https://www.crummy.com/software/BeautifulSoup/): HTMLのスクリーンスクレイピング向けに設計されたプログラムです。
- [`lxml`](https://github.com/lxml/lxml/): Python言語でXMLとHTMLを処理するための高機能で使いやすいライブラリです。
- [`html5lib`](https://github.com/html5lib/html5lib-python): PythonでHTMLドキュメントおよびフラグメントをパース/シリアライズするための標準準拠ライブラリです。

### Browser Automation
- [`selenium`](https://github.com/SeleniumHQ/selenium): ブラウザ自動化フレームワークおよびエコシステムです。
- [`playwright`](https://github.com/microsoft/playwright-python): Playwrightのテストおよび自動化ライブラリのPython版です。
- [`pyppeteer`](https://github.com/pyppeteer/pyppeteer): ヘッドレスのChrome/Chromium自動化ライブラリ（Puppeteerの非公式ポート）です。

### All-in-One Scraping
- [`scrapy`](https://github.com/scrapy/scrapy): Python向けの高速な高レベルWebクローリング＆スクレイピングフレームワークです。
- [`autoscraper`](https://github.com/alirezamika/autoscraper): Python向けのスマートで自動、かつ高速で軽量なweb scraperです。
- [`requests-html`](https://github.com/psf/requests-html): HTMLのパース（例：Webスクレイピング）をできるだけ簡単かつ直感的に行えるようにすることを目的としたライブラリです。

## Common Stacks for Scraping in Python
以下の表で、最も一般的なPython Webスクレイピングの3つのスタックを比較します：
|                               | **Requests + Beautiful Soup**                                                                            | **Selenium**                                                                                  | **Scrapy**                                                                                                                        |
| ----------------------------- | -------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| **Description**               | RequestsでWebページのHTMLコンテンツを取得し、Beautiful Soupでパースしてデータを抽出します | Webブラウザを自動化して動的サイトと対話し、データ取得やユーザー行動のシミュレーションを行います | 大規模なWebスクレイピングタスク向けの強力なフレームワークです                                                                           |
| **Requirements**              | - `requests`<br>- `beautifulsoup4`                                                                       | -  `selenium`<br>- Chrome、Firefox、EdgeなどのWebブラウザ                                | - `scrapy`                                                                                                                        |
| **Support for Static Pages**  | はい                                                                                                      | はい                                                                                           | はい                                                                                                                               |
| **Support for Dynamic Pages** | いいえ                                                                                                       | はい                                                                                           | 標準では利用できませんが、[Scrapy Splash plugin](https://github.com/scrapy-plugins/scrapy-splash)経由で利用できます |
| **Best For**                  | シンプルなスクレイピングタスク                                                                                    | ユーザー操作を必要とする動的Webサイトのスクレイピング                                       | Webクローリングを含む大規模スクレイピングプロジェクト                                                                             |

Pythonでのデータスクレイピングにおいて最も一般的なアプローチであるRequests + Beautiful Soupを使ったWebスクレイピングの方法をご覧いただく準備が整いました。

## Prerequisites
PythonでWebスクレイピングを行うには、以下が必要です：
- マシンにPython 3+がインストールされていること。
- 必要なスクレイピングライブラリをインストールできるよう、[virtual environment](https://docs.python.org/3/library/venv.html)を設定したPythonプロジェクト。

また、[Visual Studio Code with the Python extension](https://code.visualstudio.com/docs/languages/python)や[PyCharm](https://www.jetbrains.com/pycharm/)などのPython IDEを使用すると、コードの記述と管理がはるかに容易になります。

## Web Scraping with Requests and Beautiful Soup
それでは、HTTPクライアントとしてRequestsを使用し、Beautiful SoupでWebスクレイピングを行っていきます。

**Note**: 以下の例は、SeleniumベースのWebスクレイピングやScrapyベースのWebスクレイピングにも簡単に拡張できます。

専用チュートリアルについては、[Beautiful Soupによるweb scraping](https://brightdata.jp/blog/how-tos/beautiful-soup-web-scraping)のガイドをご参照ください。

### Features
RequestsとBeautiful Soupが提供する主要な機能を確認します。

#### Requests
- あらゆるメソッド（`GET`, `POST`, `PUT`, `DELETE`, `PATCH`, `HEAD`, `OPTIONS`）のHTTPリクエストをサポートします。
- HTTPヘッダー、Cookie、クエリパラメータを簡単に扱えます。
- 安全な接続のためのSSL/TLS検証をサポートします。
- サーバー提供のエンコーディングに基づくレスポンスコンテンツの自動デコード。
- Cookieと認証を維持するためのセッション処理を内蔵しています。
- HTTPエラー（[`4xx`および`5xx`のレスポンスステータスコード](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)）のエラーハンドリングを簡素化します。

#### Beautiful Soup
- HTMLおよびXMLドキュメントをPythonで読み取れる形式にパースします。
- タグ、属性、テキストを用いて要素を検索するためのメソッドを提供します。
- 高速な組み込みHTMLパーサー[`html.parser`](https://docs.python.org/3/library/html.parser.html)や、`lxml`などの外部パーサーを含む複数のパーサーをサポートします。
- 形式が不十分または壊れたHTMLでも適切に処理します。
- パースしたHTMLコンテンツのナビゲーション（および変更）を容易にします。
- Requestsおよびその他の任意の[Python HTTP client](https://brightdata.jp/blog/web-data/best-python-http-clients)とシームレスに統合でき、完全なWebスクレイピングワークフローを実現します。

### Setup
プロジェクトにRequestsとBeautiful Soupをインストールするには、有効化したvirtual environmentで次のコマンドを実行します：
```bash
pip install requests beautifulsoup4
```
その後、次のように2つのライブラリをインポートできます：
```python
import requests
from bs4 import BeautifulSoup
```
### Methods
RequestsとBeautiful Soupが提供するメソッドにより可能となる、Python Webスクレイピングで最も一般的な操作を確認します。

#### Connect to a Web Page
Requestsが公開している[`get()`](https://requests.readthedocs.io/en/latest/api/#requests.get)メソッドでWebページのHTMLを取得します：
```python
url = "https://en.wikipedia.org/wiki/Web_scraping"
response = requests.get(url)
```
`url`は対象ページのURLに置き換えてください。

内部的には、Requestsは指定されたURLに対してHTTP `GET`リクエストを実行します。Webサイトのサーバーは、ページのHTMLを含むレスポンスオブジェクトを返します。`response`を出力して確認できます：
```python
print(response)
```
出力は次のようになります：
```
<Response [200]>
```
HTTPレスポンスステータスコード[`200`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/200)は、リクエストが成功したことを意味します。

レスポンスオブジェクトからHTMLコンテンツを抽出するには、`text`属性にアクセスします：
```python
print(response.text)
```
これにより、ページのHTMLコンテンツが出力されます：
```html
<!DOCTYPE html>
<html
  class="client-nojs vector-feature-language-in-header-enabled vector-feature-language-in-main-page-header-disabled vector-feature-sticky-header-disabled vector-feature-page-tools-pinned-disabled vector-feature-toc-pinned-clientpref-1 vector-feature-main-menu-pinned-disabled vector-feature-limited-width-clientpref-1 vector-feature-limited-width-content-enabled vector-feature-custom-font-size-clientpref-1 vector-feature-appearance-pinned-clientpref-1 vector-feature-night-mode-enabled skin-theme-clientpref-day vector-toc-available"
  lang="en"
  dir="ltr"
>
  <head>
    <meta charset="UTF-8">
    <title>Web scraping - Wikipedia</title>
    <!-- omitted for brevity... -->
  </head>
</html>
```
出力は、ページの生HTMLを含む文字列です。

#### Parse an HTML String
HTML文字列は、Beautiful Soupのコンストラクタに渡すことでパースできます：
```python
soup = BeautifulSoup(html, "html.parser")
```
第1引数は、生HTMLを文字列として含む変数です。一方、第2引数はHTML処理に使用するパーサーを指定します。ここでは`html.parser`が、Python標準ライブラリが提供するデフォルトのHTMLパーサーです。

結果として得られる`soup`変数には、HTMLノードの選択、DOMの変更、選択したノード内のデータへのアクセスおよび操作を可能にするメソッドと属性が含まれます。

#### Basic Node Selection and Data Extraction Methods
ページの`<title>`要素は次のように取得できます：
```python
print(soup.title)

# OUTPUT:
# <title>Web scraping - Wikipedia</title>
```
`<title>`要素内のテキストを抽出するには、`text`属性を使用します：
```python
print(soup.title.text)

# OUTPUT:
# Web scraping - Wikipedia
```
同様に、`<h1>`要素には次のようにアクセスできます：
```python
print(soup.h1)

# OUTPUT:
# <h1 class="firstHeading mw-first-heading" id="firstHeading">
#   <span class="mw-page-title-main">Web scraping</span>
# </h1>
```python
HTML属性（例：`id`）の値を取得するには、属性名を辞書キーとしてアクセスします：
```python
print(soup.h1["id"])

# OUTPUT:
# firstHeading
```
#### Find Nodes
Beautiful SoupでHTML要素を見つけるためによく使用されるメソッドは、[`find()`と`find_all()`](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#calling-a-tag-is-like-calling-find-all)の2つです。これらのメソッドにより、HTMLドキュメント内の特定要素や要素グループを特定できます。

簡単な概要は次のとおりです：
- `find()`：最初に一致した要素を見つけます。
- `find_all()`：一致した要素すべてのリストを返します。

`find()`のシグネチャは次のようになります：
```python
find(name=None, attrs={}, recursive=True, text=None, **kwargs)
```
これは、`find()`がタグ名、属性、またはテキスト内容で検索できることを示しています。classやIDで要素を見つける場合、`**kwargs`パラメータで簡単にフィルタリングできます。

たとえば、`id="firstHeading"`の`<h1>`要素を取得するには次のように記述します：
```python
h1 = soup.find("h1", id="firstHeading")
print(h1)

# OUTPUT:
# <h1 class="firstHeading mw-first-heading" id="firstHeading">
#   <span class="mw-page-title-main">Web scraping</span>
# </h1>
```
`id`は`find()`の明示的なパラメータではありませんが、`**kwargs`の柔軟性により上記ロジックは問題なく動作します。

見出しやリンクなど、特定タイプの要素をすべて必要とする場合は、`find_all()`のほうが適しています。たとえば、すべての`<a>`タグを取得するには：
```python
links = soup.find_all("a")
print(links)

# OUTPUT:
# [
#     <a class="mw-jump-link" href="#bodyContent">Jump to content</a>,
#     <a accesskey="z" href="/wiki/Main_Page" title="Visit the main page [z]">
#         <span>Main page</span>
#     </a>,
#     <a href="/wiki/Wikipedia:Contents" title="Guides to browsing Wikipedia">
#         <span>Contents</span>
#     </a>,
#     omitted for brevity...
# ]
```
このメソッドは一致した要素のリストを返すため、簡単にループ処理して、テキスト抽出などの操作を行えます。たとえば、次のコードで一致した要素すべてのテキスト内容を抽出できます：
```python
links = soup.find_all("a")
for link in links:
  print(link.text)

# OUTPUT:
# Jump to content
# Main page
# Contents
# omitted for brevity...
```
また、タグ名と属性フィルタを組み合わせて検索範囲を絞り込むこともできます。たとえば、`class="mw-editsection"`の`<span>`タグをすべて見つけるには次のように書きます：
```python
specific_spans = soup.find_all("span", {"class": "mw-editsection"})
```
または同等に、次のようにも書けます：
```python
specific_spans = soup.find_all("span", class_="mw-editsection")
```
`class`はPythonの予約語のため、パラメータとして直接使用できません。代わりに`class_`を使用します。

どちらのアプローチも、指定条件に一致する`<span>`要素すべてのリストを返します：
```
[
    <span class="mw-editsection">
        <span class="mw-editsection-bracket">[</span>
        <a href="/w/index.php?title=Web_scraping&amp;action=edit&amp;section=1" title="Edit section: History">
            <span>edit</span>
        </a>
        <span class="mw-editsection-bracket">]</span>
    </span>,
    <span class="mw-editsection">
        <span class="mw-editsection-bracket">[</span>
        <a href="/w/index.php?title=Web_scraping&amp;action=edit&amp;section=2" title="Edit section: Techniques">
            <span>edit</span>
        </a>
        <span class="mw-editsection-bracket">]</span>
    </span>,
    <!-- omitted for brevity... -->
]
```
`find()`と`find_all()`が返すオブジェクトも、これら2つのメソッドを公開している点に注意してください。結果ノードに対して呼び出した場合、`find()`と`find_all()`のスコープはその子ノードに限定されます。
たとえば、ページの参照（references）を含むHTML要素をclassで選択します：
```python
references_element = soup.find(class_="references")
```
次に、この要素内のすべての`<li>`タグを取得し、次のように内容を出力します：
```python
list_items = references_element.find_all("li")
for item in list_items:
    print(item.text)

# OUTPUT:
# ^ Thapelo, Tsaone Swaabow; Namoshe, Molaletsa; Matsebe, Oduetse; Motshegwa, Tshiamo; Bopape, Mary-Jane Morongwa (2021-07-28). "SASSCAL WebSAPI: A Web Scraping Application Programming Interface to Support Access to SASSCAL's Weather Data". Data Science Journal. 20: 24. doi:10.5334/dsj-2021-024. ISSN 1683-1470. S2CID 237719804.
# ^ "Search Engine History.com". Search Engine History. Retrieved November 26, 2019.
# ^ Song, Ruihua; Microsoft Research (Sep 14, 2007). "Joint optimization of wrapper generation and template detection" (PDF). Proceedings of the 13th ACM SIGKDD international conference on Knowledge discovery and data mining. p. 894. doi:10.1145/1281192.1281287. ISBN 9781595936097. S2CID 833565. Archived from the original (PDF) on October 11, 2016.
# omitted for brevity...
```

#### Select Nodes
Beautiful Soupで要素を特定する別の有用なメソッドは、[`select()`](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#css-selectors-through-the-css-property)です。この関数により、[CSS selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_selectors)を使用して要素を検索できます。CSSセレクタは、タグ、class、id、その他の属性に基づいて要素を指定できる強力かつ柔軟な方法です。

たとえば、`.references`ノード内のすべての`<li>`要素は次のように取得できます：
```python
li_elements = soup.select(".references > li")
print(len(li_elements))

# OUTPUT:
# 31
```

## Export the Scraped Data
対象ページからデータをスクレイピングしたら、抽出データを含む辞書を保持していることが多いはずです。たとえば、スクレイピングしたデータを含む`titles`の辞書リストが次のようになっているとします：
```
[
    {'tag': 'h1', 'title': 'Web scraping'},
    {'tag': 'h2', 'title': 'Contents'},
    {'tag': 'h2', 'title': 'History'},
    {'tag': 'h2', 'title': 'Techniques'},
    {'tag': 'h2', 'title': 'Legal issues'},
    {'tag': 'h2', 'title': 'Methods to prevent web scraping'},
    # ...
    {'tag': 'h3', 'title': 'India'}
]
```
通常は、このデータをCSVやJSONなどの人間が読みやすい形式にエクスポートし、チームの他のメンバーが簡単にアクセスして利用できるようにしたいはずです。両形式へのエクスポート方法を見ていきましょう！

**Note**: 以下のデータエクスポートロジックは、Scrapyのようなオールインワンのスクレイピングソリューションを使用しないスクレイピングスクリプトに適用されます。理由は、ソリューション側が通常、特定の設定を通じて希望の形式に直接エクスポートするための[ビルトイン機能](https://docs.scrapy.org/en/latest/topics/feed-exports.html)を備えているためです。

### CSV Export
データをCSVにエクスポートするには、Python組み込みの[`csv`](https://docs.python.org/3/library/csv.html)モジュールを使用できます。このモジュールにより、データを`.csv`ファイルへ書き込めます。辞書の各キーが列ヘッダーに対応し、値が対応する行になります。

まず、[`open()`](https://docs.python.org/3/library/functions.html#open)関数を使用して、書き込み先のCSVファイル`titles.csv`を開きます：
```python
with open("titles.csv", mode="w", newline="", encoding="utf-8") as file:
```
この場合、`"w"`はファイルへの書き込みを意味し、`newline=""`は行の間に余分な空行が入らないようにして正しく行を書き込むことを保証します。操作完了後にファイルが適切にクローズされるようにする[`with` statement](https://docs.python.org/3/reference/compound_stmts.html#with)の使用に注意してください。

次に、[`DictWriter`](https://docs.python.org/3/library/csv.html#csv.DictWriter)クラスを使用して、辞書キーに対応するヘッダーを書き込みます：
```python
writer = csv.DictWriter(file, fieldnames=["tag", "title"])
writer.writeheader()
```
ヘッダーの後は、辞書リストを反復しながら`writer.writerow()`メソッドでデータ自体を書き込みます：
```python
for row in titles:
    writer.writerow(row)
```
上記ロジックにより、キーが列に対応し、値が辞書からの実データとなる行全体が書き込まれます。

最後に、`with` statementが書き込み後のファイルクローズを自動的に処理します。

出力は次のようになります：
```csv
tag,title
h1,Web scraping
h2,Contents
h2,History
h2,Techniques
h2,Legal issues
h2,Methods to prevent web scraping
h2,See also
h2,References
h3,Human copy-and-paste
h3,Text pattern matching
h3,HTTP programming
h3,HTML parsing
h3,DOM parsing
h3,Vertical aggregation
h3,Semantic annotation recognizing
h3,Computer vision web-page analysis
h3,AI-powered document understanding
h3,United States
h3,European Union
h3,Australia
h3,India
```
同じ結果は、リポジトリ内の`titles.csv`ファイルでも確認できます。

### JSON Export
スクレイピングしたデータをJSONにエクスポートするには、Python組み込みの[`json`](https://docs.python.org/3/library/json.html)モジュールを利用できます。このモジュールにより、Python辞書をJSON形式の文字列に変換して`.json`ファイルに書き込めます。

まず、`open()`関数を使用して書き込み用のJSONファイル`titles.json`を開きます：
```python
with open("titles.json", mode="w", encoding="utf-8") as file:
```
ここでも、`with` statementにより操作完了後にファイルが自動的にクローズされます。

次に、`json.dump()`関数を使用して辞書をJSON形式に変換し、ファイルへ書き込みます：
```python
json.dump(titles, file, indent=4)
```
`indent=4`引数により、JSONデータがインデント4スペースで整形出力され、人間が読みやすくなります。

出力は次のようになります：
```json
[
    {
        "tag": "h1",
        "title": "Web scraping"
    },
    {
        "tag": "h2",
        "title": "Contents"
    },
    {
        "tag": "h2",
        "title": "History"
    },
    {
        "tag": "h2",
        "title": "Techniques"
    },
    {
        "tag": "h2",
        "title": "Legal issues"
    },
    {
        "tag": "h2",
        "title": "Methods to prevent web scraping"
    },
    {
        "tag": "h2",
        "title": "See also"
    },
    {
        "tag": "h2",
        "title": "References"
    },
    {
        "tag": "h3",
        "title": "Human copy-and-paste"
    },
    {
        "tag": "h3",
        "title": "Text pattern matching"
    },
    {
        "tag": "h3",
        "title": "HTTP programming"
    },
    {
        "tag": "h3",
        "title": "HTML parsing"
    },
    {
        "tag": "h3",
        "title": "DOM parsing"
    },
    {
        "tag": "h3",
        "title": "Vertical aggregation"
    },
    {
        "tag": "h3",
        "title": "Semantic annotation recognizing"
    },
    {
        "tag": "h3",
        "title": "Computer vision web-page analysis"
    },
    {
        "tag": "h3",
        "title": "AI-powered document understanding"
    },
    {
        "tag": "h3",
        "title": "United States"
    },
    {
        "tag": "h3",
        "title": "European Union"
    },
    {
        "tag": "h3",
        "title": "Australia"
    },
    {
        "tag": "h3",
        "title": "India"
    }
]
```
同じ結果は、リポジトリ内の`titles.json`ファイルでも確認できます。

## Web Scraping Examples in Python
["Web Scraping" Wikipedia page](https://en.wikipedia.org/wiki/Web_scraping)から、すべての`<hX>`（`X`は`1`、`2`、`3`、`4`、または`5`）のタイトル要素をスクレイピングしてCSVにエクスポートしたいとします。以下でどのように実現できるかをご覧ください：
1. Requests + Beautiful Soup
2. Selenium
3. Scrapy

それでは、PythonでWebスクレイピングを実行しましょう！

### 1. Requests + Beautiful Soup
```python
import requests
from bs4 import BeautifulSoup
import csv

# URL of the page to scrape
url = "https://en.wikipedia.org/wiki/Web_scraping"

# Send a GET request to the URL and get the response
response = requests.get(url)

# Get the HTML content of the page
html = response.text

# Parse the HTML content with BeautifulSoup
soup = BeautifulSoup(html, "html.parser")

# List where to store the scraped titles
titles = []

# List of header levels (h1, h2, h3, h4, h5)
title_level_list = [1, 2, 3, 4, 5]

# Loop through each header level (h1, h2, h3, h4, h5)
for title_level in title_level_list:
    # Find all elements of the current header level
    title_elements = soup.find_all(f"h{title_level}")

    # Loop through each title element found
    for title_element in title_elements:
        # Data extraction logic
        tag = title_element.name
        text = title_element.text

        # Create a dictionary with the tag and the title text
        title = {
            "tag": tag,
            "title": text,
        }

        # Append the dictionary to the titles list
        titles.append(title)

# Open a CSV file to write the data
with open("titles.csv", mode="w", newline="", encoding="utf-8") as file:
    # Create a CSV writer object and specify the fieldnames (columns)
    writer = csv.DictWriter(file, fieldnames=["tag", "title"])

    # Write the header (column names) to the CSV file
    writer.writeheader()

    # Write each row (dictionary) to the CSV file
    for row in titles:
        writer.writerow(row)
```
同じロジックは`requests-beautifulsoup-scraper.py`ファイルで確認できます。

### 2. Selenium
```python
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.chrome.options import Options
from selenium.webdriver.common.by import By
import csv

# Set up the WebDriver that operates in headless mode
options = Options()
options.add_argument("--headless")
driver = webdriver.Chrome(service=Service(), options=options)

# URL of the page to scrape
url = "https://en.wikipedia.org/wiki/Web_scraping"

# Open the URL in the browser
driver.get(url)

# List to store the scraped titles
titles = []

# List of header levels (h1, h2, h3, h4, h5)
title_level_list = [1, 2, 3, 4, 5]

# Loop through each header level (h1, h2, h3, h4, h5)
for title_level in title_level_list:
    # Find all elements of the current header level using a CSS Selector
    title_elements = driver.find_elements(By.CSS_SELECTOR, f"h{title_level}")

    # Loop through each title element found
    for title_element in title_elements:
        # Data extraction logic
        tag = title_element.tag_name
        text = title_element.text

        # Create a dictionary with the tag and the title text
        title = {
            "tag": tag,
            "title": text,
        }

        # Append the dictionary to the titles list
        titles.append(title)

# Close the browser
driver.quit()

# Open a CSV file to write the data
with open("titles.csv", mode="w", newline="", encoding="utf-8") as file:
    # Create a CSV writer object and specify the fieldnames (columns)
    writer = csv.DictWriter(file, fieldnames=["tag", "title"])

    # Write the header (column names) to the CSV file
    writer.writeheader()

    # Write each row (dictionary) to the CSV file
    for row in titles:
        writer.writerow(row)
```
同じロジックは`selenium-scraper.py`ファイルで確認できます。

### Scrapy
まず、Scrapyプロジェクトを初期化します：
```bash
scrapy startproject scrapy_scraping
```
次に、`scrapy_scraping`フォルダに入り、目的のページをターゲットとする「wikipedia」という新しいSpiderを作成します：
```bash
cd scrapy_scraping
scrapy genspider wikipedia https://en.wikipedia.org/wiki/Web_scraping
```
`wikipedia.py`ファイルが`scrapy_scraping/scrapy_scraping/spiders`フォルダに作成されます：
```python
import scrapy


class WikipediaSpider(scrapy.Spider):
    name = "wikipedia"
    allowed_domains = ["en.wikipedia.org"]
    start_urls = ["https://en.wikipedia.org/wiki/Web_scraping"]

    def parse(self, response):
        pass
```
スクレイピングロジックを実装します：
```python
import scrapy


class WikipediaSpider(scrapy.Spider):
    name = "wikipedia"
    allowed_domains = ["en.wikipedia.org"]
    start_urls = ["https://en.wikipedia.org/wiki/Web_scraping"]

    def parse(self, response):
        # List to store the titles
        titles = []

        # List of header levels (h1, h2, h3, h4, h5)
        title_level_list = [1, 2, 3, 4, 5]

        # Loop through each header level (h1, h2, h3, h4, h5)
        for title_level in title_level_list:
            # Find all elements of the current header level
            title_elements = response.css(f"h{title_level}")

            # Loop through each title element found
            for title_element in title_elements:
                # Extract tag and text
                tag = title_element.root.tag
                text = title_element.css("::text").get().strip()

                # Yield the data directly to the feed
                yield {
                    "tag": tag,
                    "title": text,
                }
```
次のコマンドでSpiderを実行してデータをスクレイピングし、`titles.csv`ファイルにエクスポートできます：
```bash
scrapy crawl wikipedia -o titles.csv
```
このScrapyプロジェクトは、repoの`scrapy_scraping`フォルダで確認できます。

## Challenges of Python Web Scraping
Webスクレイピングは、このリポジトリで示したように常に簡単とは限りません。多くのWebサイトは、ページ上で一般公開されている場合でもデータの価値を理解しているため、スクレイパーがページにアクセスしてデータを抽出するのを防ぐために、複数の[アンチスクレイピング対策](https://brightdata.jp/blog/web-data/anti-scraping-techniques)を実装しています。

特に効果的な方法には、CAPTCHA、ブラウザフィンガープリント、TLSフィンガープリント、レート制限、IPブロッキングがあります。回避策によってこれらをバイパスできる場合もありますが、いたちごっこのような状況であり、多くの手法は一時的で、常に信頼できるとは限りません。

解決策はあるのでしょうか？ 続きをお読みください！

## Simplified Web Scraping With Web Scraper API
[Bright Data's Web Scraper API](https://brightdata.jp/products/web-scraper)は、著名なeコマースやソーシャルメディアプラットフォームを含む100以上の人気ドメインから、構造化データを抽出するための効率的かつスケーラブルなソリューションを提供します。対応ドメインの一覧には、世界で最も訪問されているサイトの一部が含まれています。

専用エンドポイントにより、このAPIは高品質でコンプライアンスに準拠したデータへシームレスにアクセスできます。本ツールの主な機能は次のとおりです：
- バルクリクエスト処理（1リクエストあたり最大5,000 URL）。
- JSON、CSV、その他の形式へのデータエクスポート。
- 任意のプログラミング言語およびHTTPクライアントツールとの統合。
- より高速なデータ収集のための、無制限の同時接続スクレイピングタスク。
- 99.9%の稼働率。
- ブロックを回避するための自動IPローテーション、CAPTCHA解決、JavaScriptレンダリング。
- 195か国で7,200万以上のIPを持つレジデンシャルプロキシネットワークとのビルトイン統合。

Web Scraper APIにより、Python（または他の任意のプログラミング言語）でのWebスクレイピングは、単純なAPI呼び出しに集約されます。[official documentation](https://docs.brightdata.com/scraping-automation/web-data-apis/web-scraper-api/overview)にある統合ガイドをご確認ください。