---
title: VS Code 用 Docs Authoring Pack
description: この記事では、docs.microsoft.com の Markdown の作成を促進する VS Code 拡張パックについて説明します。
author: meganbradley
ms.author: mbradley
manager: jemash
ms.date: 04/06/2018
ms.prod: non-product-specific
ms.topic: contributor-guide
ms.custom: external-contributor-guide
ms.openlocfilehash: d0d61db2faf88598ecd2c800fb5fbe8df8ec44f5
ms.sourcegitcommit: 7b668124f25b8ad0442937a3ad05b19a47af5970
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="docs-authoring-pack-for-vs-code"></a><span data-ttu-id="26258-103">VS Code 用 Docs Authoring Pack</span><span class="sxs-lookup"><span data-stu-id="26258-103">Docs Authoring Pack for VS Code</span></span>

<span data-ttu-id="26258-104">Docs Authoring Pack は、docs.microsoft.com の Markdown の作成を支援する VS Code 拡張機能の集まりです。このパックは、[VS Code Marketplace で入手可能であり](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack)、次の拡張機能を含んでいます。</span><span class="sxs-lookup"><span data-stu-id="26258-104">The Docs Authoring Pack is a collection of VS Code extensions to aid with Markdown authoring for docs.microsoft.com. The pack is [available in the VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) and contains the following extensions:</span></span>

- <span data-ttu-id="26258-105">**DocFx:** docs.microsoft.com 固有の Markdown のプレビューを含んでいます。</span><span class="sxs-lookup"><span data-stu-id="26258-105">**DocFx:** Provides a docs.microsoft.com-specific Markdown preview.</span></span> <span data-ttu-id="26258-106">詳細については、[DocFx](https://marketplace.visualstudio.com/items?itemName=ms-docfx.DocFX) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="26258-106">For more information, see [DocFx](https://marketplace.visualstudio.com/items?itemName=ms-docfx.DocFX).</span></span>
- <span data-ttu-id="26258-107">**markdownlint:** David Anson 氏による人気のある Markdown リンターで、ベスト プラクティスに従った Markdown を作成するために役立ちます。</span><span class="sxs-lookup"><span data-stu-id="26258-107">**markdownlint:** A popular Markdown linter by David Anson to help ensure your Markdown follows best practices.</span></span> <span data-ttu-id="26258-108">詳細については、[markdownlint](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="26258-108">For more information, see [markdownlint](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint).</span></span>
- <span data-ttu-id="26258-109">**Docs Markdown:** Open Publishing System (OPS) での docs.microsoft.com コンテンツの Markdown 作成サポートを提供します。OPS での基本的な Markdown のサポートとカスタム Markdown 構文のサポートが含まれます。</span><span class="sxs-lookup"><span data-stu-id="26258-109">**Docs Markdown:** Provides Markdown authoring assistance for docs.microsoft.com content in the Open Publishing System (OPS), including basic Markdown support and support for custom Markdown syntax in OPS.</span></span> <span data-ttu-id="26258-110">このトピックの残りの部分では、Docs Markdown の拡張機能について説明します。</span><span class="sxs-lookup"><span data-stu-id="26258-110">The rest of this topic describes the Docs Markdown extension.</span></span>

## <a name="prerequisites-and-assumptions"></a><span data-ttu-id="26258-111">前提条件</span><span class="sxs-lookup"><span data-stu-id="26258-111">Prerequisites and assumptions</span></span>

<span data-ttu-id="26258-112">Docs Markdown 拡張機能を使用して、相対リンク、画像、その他の埋め込みコンテンツを正確に挿入するには、複製された OPS リポジトリのルートを対象範囲とした VS Code ワークスペースを持っている必要があります。</span><span class="sxs-lookup"><span data-stu-id="26258-112">To accurately insert relative links, images, and other embedded content with the Docs Markdown extension, you must have your VS Code workspace scoped to the root of your cloned OPS repo.</span></span>

<span data-ttu-id="26258-113">アラートやスニペットなどの拡張機能でサポートされる一部の構文は、OPS のカスタム Markdown であり、OPS を介して公開されない限り正しくレンダリングされません。</span><span class="sxs-lookup"><span data-stu-id="26258-113">Some syntax supported by the extension, such as alerts and snippets, are custom Markdown for OPS, and will not render correctly unless published via OPS.</span></span>

## <a name="how-to-use-the-docs-markdown-extension"></a><span data-ttu-id="26258-114">Docs Markdown 拡張機能の使用方法</span><span class="sxs-lookup"><span data-stu-id="26258-114">How to use the Docs Markdown extension</span></span>

<span data-ttu-id="26258-115">Docs Markdown のメニューにアクセスするには、「`ALT+M`」と入力します。</span><span class="sxs-lookup"><span data-stu-id="26258-115">To access the Docs Markdown menu, type `ALT+M`.</span></span> <span data-ttu-id="26258-116">上下の矢印をクリックまたは使用して、必要な機能を選択するか、フィルターの入力して開始し、メニューで必要な機能が強調表示されたら `ENTER` キーを押します。</span><span class="sxs-lookup"><span data-stu-id="26258-116">You can click or use up/down arrows to select the function you want, or type to start filtering, then hit `ENTER` when the function you want is highlighted in the menu.</span></span> <span data-ttu-id="26258-117">次の機能を使用できます:</span><span class="sxs-lookup"><span data-stu-id="26258-117">The following are available:</span></span>

|<span data-ttu-id="26258-118">機能</span><span class="sxs-lookup"><span data-stu-id="26258-118">Function</span></span>     |<span data-ttu-id="26258-119">コマンド</span><span class="sxs-lookup"><span data-stu-id="26258-119">Command</span></span>             |<span data-ttu-id="26258-120">説明</span><span class="sxs-lookup"><span data-stu-id="26258-120">Description</span></span>           |
|-------------|--------------------|----------------------|
|<span data-ttu-id="26258-121">太字</span><span class="sxs-lookup"><span data-stu-id="26258-121">Bold</span></span>         |`formatBold`        |<span data-ttu-id="26258-122">テキストを**太字**に書式設定します。</span><span class="sxs-lookup"><span data-stu-id="26258-122">Formats text **bold**.</span></span>|
|<span data-ttu-id="26258-123">斜体</span><span class="sxs-lookup"><span data-stu-id="26258-123">Italic</span></span>       |`formatItalic`      |<span data-ttu-id="26258-124">テキストを*斜体*に書式設定します。</span><span class="sxs-lookup"><span data-stu-id="26258-124">Formats text *italic*.</span></span>|
|<span data-ttu-id="26258-125">コード</span><span class="sxs-lookup"><span data-stu-id="26258-125">Code</span></span>         |`formatCode`        |<span data-ttu-id="26258-126">1 つ以下の線が選択されているときに、テキストを `inline code` として書式設定します。</span><span class="sxs-lookup"><span data-stu-id="26258-126">If one line or less is selected, formats text as `inline code`.</span></span><br><br><span data-ttu-id="26258-127">複数の線が選択されている場合、それらをフェンスされたコードのブロックとして書式設定します。オプションで OPS でサポートされているプログラミング言語を選択できます。</span><span class="sxs-lookup"><span data-stu-id="26258-127">If multiple lines are selected, formats them as a fenced code block, and allows you to optionally select a programming language supported by OPS.</span></span>|
|<span data-ttu-id="26258-128">アラート</span><span class="sxs-lookup"><span data-stu-id="26258-128">Alert</span></span>        |`insertAlert`       |<span data-ttu-id="26258-129">メモ、重要、警告、またはヒントを挿入します。</span><span class="sxs-lookup"><span data-stu-id="26258-129">Inserts a Note, Important, Warning, or Tip.</span></span><br><br><span data-ttu-id="26258-130">メニューからアラートを選択し、アラートの種類を選択します。</span><span class="sxs-lookup"><span data-stu-id="26258-130">Select Alert from the menu, then select the alert type.</span></span> <span data-ttu-id="26258-131">以前にテキストを選択している場合は、選択したアラートの構文でテキストが囲まれます。</span><span class="sxs-lookup"><span data-stu-id="26258-131">If you have previously selected text, it will be surrounded with the selected alert syntax.</span></span> <span data-ttu-id="26258-132">テキストを選択していない場合は、プレースホルダーのテキストと共にアラートが追加されます。</span><span class="sxs-lookup"><span data-stu-id="26258-132">If no text is selected, a new alert will be added with placeholder text.</span></span>|
|<span data-ttu-id="26258-133">番号付きリスト</span><span class="sxs-lookup"><span data-stu-id="26258-133">Numbered list</span></span>|`insertNumberedList` |<span data-ttu-id="26258-134">新しい番号付きリストを挿入します。</span><span class="sxs-lookup"><span data-stu-id="26258-134">Inserts a new numbered list.</span></span><br><br> <span data-ttu-id="26258-135">複数の行が選択されている場合は、各行がリスト項目になります。</span><span class="sxs-lookup"><span data-stu-id="26258-135">If multiple lines are selected, each will be a list item.</span></span> <span data-ttu-id="26258-136">Markdown 内の番号付きリストはすべて 1 として表示されますが、docs.microsoft.com では連番、または入れ子になったリストでは文字としてレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="26258-136">Note that numbered lists show in the Markdown as all 1s, but will render on docs.microsoft.com as sequential numbers or, for nested lists, letters.</span></span> <span data-ttu-id="26258-137">入れ子になった番号付きリストを作成するには、親リスト内からタブを指定します。</span><span class="sxs-lookup"><span data-stu-id="26258-137">To create a nested numbered list, tab from within the parent list.</span></span>|
|<span data-ttu-id="26258-138">箇条書き</span><span class="sxs-lookup"><span data-stu-id="26258-138">Bulleted list</span></span>|`insertBulletedList` |<span data-ttu-id="26258-139">新しい箇条書きを挿入します。</span><span class="sxs-lookup"><span data-stu-id="26258-139">Inserts a new bulleted list.</span></span>|
|<span data-ttu-id="26258-140">テーブル</span><span class="sxs-lookup"><span data-stu-id="26258-140">Table</span></span>        |`insertTable`        |<span data-ttu-id="26258-141">Markdown のテーブル構造を挿入します。</span><span class="sxs-lookup"><span data-stu-id="26258-141">Inserts a Markdown table structure.</span></span><br><br><span data-ttu-id="26258-142">テーブル コマンドを選択した後で、3:4 のように列:行の形式で列と行の数を指定します。</span><span class="sxs-lookup"><span data-stu-id="26258-142">After you select the table command, specify the number of columns and rows in the format columns:rows, such as 3:4.</span></span> <span data-ttu-id="26258-143">この式で指定できる列の最大数は 5 です。読みやすくするためにこの最大数が推奨されます。</span><span class="sxs-lookup"><span data-stu-id="26258-143">Note that the maximum number of columns you can specify via this extension is 5, which is the recommended maximum for readability.</span></span>|
|<span data-ttu-id="26258-144">リンク</span><span class="sxs-lookup"><span data-stu-id="26258-144">Link</span></span>         |`selectLinkType`      |<span data-ttu-id="26258-145">リンクを挿入します。</span><span class="sxs-lookup"><span data-stu-id="26258-145">Inserts a link.</span></span> <span data-ttu-id="26258-146">このコマンドを選択すると、次のサブメニューが表示されます。</span><span class="sxs-lookup"><span data-stu-id="26258-146">When you select this command, the following sub-menu appears.</span></span><br><br><span data-ttu-id="26258-147">`External`: URI で Web ページにリンクします。</span><span class="sxs-lookup"><span data-stu-id="26258-147">`External`: Link to a web page by URI.</span></span> <span data-ttu-id="26258-148">"http" または "https" を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="26258-148">Must include "http" or "https".</span></span><br><span data-ttu-id="26258-149">`Internal`: 同じリポジトリ内の別のファイルへの相対リンクを挿入します。</span><span class="sxs-lookup"><span data-stu-id="26258-149">`Internal`: Insert a relative link to another file in the same repo.</span></span> <span data-ttu-id="26258-150">このオプションを選択した後で、コマンド ウィンドウに入力し、名前でフィルター処理し、必要なファイルを選択します。</span><span class="sxs-lookup"><span data-stu-id="26258-150">After selecting this option, type in the command window to filter files by name, then select the file you want.</span></span> <br><span data-ttu-id="26258-151">`Bookmark in this file`: 現在のファイルの見出しの一覧から選択し、適切に書式設定されたブックマークを挿入します。</span><span class="sxs-lookup"><span data-stu-id="26258-151">`Bookmark in this file`: Choose from a list of headings in the current file to insert a properly formatted bookmark.</span></span><br><span data-ttu-id="26258-152">`Bookmark in another file`: 最初に、ファイル名でフィルター処理して、リンク先のファイルを選択し、次に選択したファイル内の適切な見出しを選択します。</span><span class="sxs-lookup"><span data-stu-id="26258-152">`Bookmark in another file`: First, filter by file name and select the file to link to, then choose the appropriate heading within the selected file.</span></span>|
|<span data-ttu-id="26258-153">イメージ</span><span class="sxs-lookup"><span data-stu-id="26258-153">Image</span></span>        |`insertImage`     |<span data-ttu-id="26258-154">代替テキスト (アクセシビリティのために必要) を入力してそれを選択し、このコマンドを実行してリポジトリ内のサポートされる画像ファイルのリストをフィルター処理し、必要なファイルを選択します。</span><span class="sxs-lookup"><span data-stu-id="26258-154">Type alternate text (required for accessibility) and select it, then call this command to filter the list of supported image files in the repo and select the one you want.</span></span> <span data-ttu-id="26258-155">このコマンドを呼び出したときに代替テキストを選択していない場合、画像ファイルを選択する前に代替テキストを選択するように指示されます。</span><span class="sxs-lookup"><span data-stu-id="26258-155">If you haven't selected alt text when you call this command, you will be prompted for it before you can select an image file.</span></span>|
|<span data-ttu-id="26258-156">含める</span><span class="sxs-lookup"><span data-stu-id="26258-156">Include</span></span>      |`insertInclude`   |<span data-ttu-id="26258-157">現在のファイル内に埋め込むファイルを見つけます。</span><span class="sxs-lookup"><span data-stu-id="26258-157">Find a file to embed in the current file.</span></span>|
|<span data-ttu-id="26258-158">スニペット</span><span class="sxs-lookup"><span data-stu-id="26258-158">Snippet</span></span>      |`insertSnippet`   |<span data-ttu-id="26258-159">現在のファイル内に埋め込むリポジトリ内のコード スニペットを見つけます。</span><span class="sxs-lookup"><span data-stu-id="26258-159">Find a code snippet in the repo to embed in the current file.</span></span>|
|<span data-ttu-id="26258-160">ビデオ</span><span class="sxs-lookup"><span data-stu-id="26258-160">Video</span></span>        |`insertVideo`     |<span data-ttu-id="26258-161">埋め込みビデオを追加します。</span><span class="sxs-lookup"><span data-stu-id="26258-161">Add an embedded video.</span></span>|
|<span data-ttu-id="26258-162">プレビュー</span><span class="sxs-lookup"><span data-stu-id="26258-162">Preview</span></span>      |`previewTopic`    |<span data-ttu-id="26258-163">DocFX 拡張機能を使用し、左右に並べたウィンドウにアクティブなトピックのプレビューを表示します。</span><span class="sxs-lookup"><span data-stu-id="26258-163">Preview the active topic in a side-by-side window using the DocFX extension.</span></span>  <span data-ttu-id="26258-164">DocFX 拡張機能がインストールされていない場合またはインストールされていても無効になっている場合、トピックはレンダリングされません。</span><span class="sxs-lookup"><span data-stu-id="26258-164">If the DocFX extension is not installed or is installed but disabled, the topic will not render.</span></span>


## <a name="how-to-assign-keyboard-shortcuts"></a><span data-ttu-id="26258-165">キーボード ショートカットの割り当て方法</span><span class="sxs-lookup"><span data-stu-id="26258-165">How to assign keyboard shortcuts</span></span>

1. <span data-ttu-id="26258-166">「`CTRL+K`」と入力し、「`CTRL+S`」と入力してキーボード ショートカットの一覧を開きます。</span><span class="sxs-lookup"><span data-stu-id="26258-166">Type `CTRL+K` then `CTRL+S` to open the Keyboard Shortcuts list.</span></span>
1. <span data-ttu-id="26258-167">カスタム キーバインドを作成するコマンド (`formatBold` など) を検索します。</span><span class="sxs-lookup"><span data-stu-id="26258-167">Search for the command, such as `formatBold`, for which you want to create a custom keybinding.</span></span>
1. <span data-ttu-id="26258-168">マウス ポインターを行の上に置いたときにコマンド名の近くに表示されるプラス記号をクリックします。</span><span class="sxs-lookup"><span data-stu-id="26258-168">Click the plus that appears near the command name when you mouse over the line.</span></span>
1. <span data-ttu-id="26258-169">新しい入力ボックスが表示されたら、特定のコマンドにバインドするキーボード ショートカットを入力します。</span><span class="sxs-lookup"><span data-stu-id="26258-169">After a new input box is visible, type the keyboard shortcut you want to bind to that particular command.</span></span> <span data-ttu-id="26258-170">たとえば、太字の共通のショートカットを使用するには、「`ctrl+b`」と入力します。</span><span class="sxs-lookup"><span data-stu-id="26258-170">For example, to use the common shortcut for bold, type `ctrl+b`.</span></span>
1. <span data-ttu-id="26258-171">Markdown 以外のファイルで使用できないようにするために、`when` 句をキーバインドに含めることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="26258-171">It's a good idea to insert a `when` clause into your keybinding, so it won't be available in files other than Markdown.</span></span> <span data-ttu-id="26258-172">これを行うには、*keybindings.json* を開き、コマンド名の下に次の行を挿入します (必ず行の間にコマンドを追加してください)。</span><span class="sxs-lookup"><span data-stu-id="26258-172">To do this, open *keybindings.json* and insert the following line below the command name (be sure to add a comma between lines):</span></span>
   
    `"when": "editorTextFocus && editorLangId == 'markdown'"`

    <span data-ttu-id="26258-173">keybindings.json 内の完成したキーバインドは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="26258-173">Your completed custom keybinding should look like this in keybindings.json:</span></span>

    ```json
    // Place your key bindings in this file to overwrite the defaults
    [
        {
            "key": "ctrl+b",
            "command": "formatBold",
            "when": "editorTextFocus && editorLangId == 'markdown'"
        }
    ]
    ```

1. <span data-ttu-id="26258-174">keybindings.json を保存します。</span><span class="sxs-lookup"><span data-stu-id="26258-174">Save keybindings.json.</span></span>

<span data-ttu-id="26258-175">詳細については、VS Code のドキュメントの[キーバインド](https://code.visualstudio.com/docs/getstarted/keybindings)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="26258-175">See [Keybindings](https://code.visualstudio.com/docs/getstarted/keybindings) in the VS Code docs for more information.</span></span>

## <a name="how-to-show-the-legacy-gauntlet-toolbar"></a><span data-ttu-id="26258-176">レガシーの "Gauntlet" ツールバーの表示方法</span><span class="sxs-lookup"><span data-stu-id="26258-176">How to show the legacy "Gauntlet" toolbar</span></span>

<span data-ttu-id="26258-177">"Gauntlet" という名前の拡張コードの以前のユーザーは、Docs Markdown 拡張機能がインストールされたときに VS Code ウィンドウの下部にオーサリング ツールバーが表示されなくなったことに気付くでしょう。</span><span class="sxs-lookup"><span data-stu-id="26258-177">Former users of the extension code-named "Gauntlet" will notice that the authoring toolbar no longer appears at the bottom of the VS Code window when the Docs Markdown Extension is installed.</span></span> <span data-ttu-id="26258-178">これは、ツールバーが VS Code ステータス バー上で多くの領域を使用し、拡張機能のユーザー エクスペリエンスのベスト プラクティスに従っていなかったために新しい拡張機能で非推奨になったためです。</span><span class="sxs-lookup"><span data-stu-id="26258-178">This is because the toolbar took up a lot of space on the VS Code status bar and did not follow best practices for extension UX, so it is deprecated in the new extension.</span></span> <span data-ttu-id="26258-179">しかし、オプションで VS Code の settings.json ファイルを次のように更新することでツールバーを表示できます。</span><span class="sxs-lookup"><span data-stu-id="26258-179">However, you can optionally show the toolbar by updating your VS Code settings.json file as follows:</span></span>

1. <span data-ttu-id="26258-180">VS Code で、[ファイル]、[基本設定]、[設定] (`CTRL+Comma`) の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="26258-180">In VS Code, go to File -> Preferences -> Settings (`CTRL+Comma`).</span></span>
1. <span data-ttu-id="26258-181">[ユーザー設定] を選択してすべての VS Code ワークスペースの設定を変更するか、[ワークスペースの設定] を選択して、現在のワークスペースのみの設定を変更します。</span><span class="sxs-lookup"><span data-stu-id="26258-181">Select User Settings to change the settings for all VS Code workspaces, or  Workspace Settings to change them for just the current workspace.</span></span>
1. <span data-ttu-id="26258-182">[既定の設定] ウィンドウで、[Docs Authoring Extension Configuration]\(Docs Authoring 拡張機能の構成\) を見つけ、目的の設定の横にある鉛筆アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="26258-182">In the Default Settings pane, find Docs Authoring Extension Configuration, and select the pencil icon next to the desired setting.</span></span> <span data-ttu-id="26258-183">次に、`true` または `false` を選択するように指示されます。</span><span class="sxs-lookup"><span data-stu-id="26258-183">Next, you will be prompted to select either `true` or `false`.</span></span> <span data-ttu-id="26258-184">選択すると、VS Code によって settings.json ファイルに自動的に値が追加され、変更を有効にするためにウィンドウを再び読み込むように指示されます。</span><span class="sxs-lookup"><span data-stu-id="26258-184">Once you've made your selection, VS Code will automatically add the value to the settings.json file and you will be prompted to reload the window for the changes to take effect.</span></span>

## <a name="known-issues"></a><span data-ttu-id="26258-185">既知の問題</span><span class="sxs-lookup"><span data-stu-id="26258-185">Known issues</span></span>

- <span data-ttu-id="26258-186">DocFX Preview: MacOS および Linux: DocFX Preview でプレビューが正しく起動しない (これらのプラットフォームではプレビューは既定で VS Code Markdown プレビューになります)。</span><span class="sxs-lookup"><span data-stu-id="26258-186">DocFX Preview: On MacOS and Linux, DocFX Preview does not launch preview correctly (preview defaults to VS Code Markdown preview for these platforms).</span></span>
- <span data-ttu-id="26258-187">DocFx Preview: すべてのプラットフォームで API への xref (相互参照) リンクなどの一部の構文が、プレビューで正しくレンダリングされない。場合によってはコンテンツ ページが閉じる。</span><span class="sxs-lookup"><span data-stu-id="26258-187">DocFx Preview: On all platforms, some syntax, such as xref (cross-reference) links to APIs, do not render correctly in preview, in some cases leaving content gaps.</span></span>
- <span data-ttu-id="26258-188">外部ブックマーク: Linux でファイル リストが表示されるが、見出しが表示されない。</span><span class="sxs-lookup"><span data-stu-id="26258-188">External bookmarks: On Linux, the file list is displayed but no headings are shown to select.</span></span>
- <span data-ttu-id="26258-189">含む: Linux でファイル リストが表示されるが、選択を行った後でリンクが追加されない。</span><span class="sxs-lookup"><span data-stu-id="26258-189">Includes: On Linux, the file list is displayed but no link is added after selection is made.</span></span>