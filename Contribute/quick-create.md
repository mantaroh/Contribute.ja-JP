---
title: 'クイック スタート: Azure Key Vault でのシークレットの設定と取得 | Microsoft Docs'
description: 'クイック スタート: Azure Key Vault でのシークレットの設定と取得'
services: key-vault
author: syntaxc4
manager: erifkin
ms.date: 07/24/2018
ms.author: cfowler
zone_pivot_groups: keyvault-languages, keyvault-platforms
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: 8b758274203748bb6e04c03dec5de38fb77947b4
ms.sourcegitcommit: b0105f322f91bb4dbde47f6da35b3c12271d5b03
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2018
ms.locfileid: "43239561"
---
# <a name="quickstart-set-and-retrieve-a-secret-from-azure-key-vault"></a><span data-ttu-id="282d0-103">クイック スタート: Azure Key Vault でのシークレットの設定と取得</span><span class="sxs-lookup"><span data-stu-id="282d0-103">Quickstart: Set and retrieve a secret from Azure Key Vault</span></span>

<span data-ttu-id="282d0-104">このクイック スタートでは、Web アプリを使って Key Vault にシークレットを格納する方法とシークレットを取得する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="282d0-104">This quickstart shows you how to store a secret in Key Vault and how to retrieve it using a Web app.</span></span> <span data-ttu-id="282d0-105">シークレット値を確認するには、Azure でこれを実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="282d0-105">To see the secret value you would have to run this on Azure.</span></span> <span data-ttu-id="282d0-106">このクイック スタートでは Node.js とマネージド サービス ID (MSI) を使用します。</span><span class="sxs-lookup"><span data-stu-id="282d0-106">The quickstart uses Node.js and Managed service identities (MSIs)</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="282d0-107">キー コンテナーを作成します。</span><span class="sxs-lookup"><span data-stu-id="282d0-107">Create a Key Vault.</span></span>
> * <span data-ttu-id="282d0-108">キー コンテナーにシークレットを格納します。</span><span class="sxs-lookup"><span data-stu-id="282d0-108">Store a secret in Key Vault.</span></span>
> * <span data-ttu-id="282d0-109">キー コンテナーからシークレットを取得します。</span><span class="sxs-lookup"><span data-stu-id="282d0-109">Retrieve a secret from Key Vault.</span></span>
> * <span data-ttu-id="282d0-110">Azure AD Web アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="282d0-110">Create an Azure Web Application.</span></span>
> * <span data-ttu-id="282d0-111">[マネージド サービス ID を有効にします](https://docs.microsoft.com/azure/active-directory/managed-service-identity/overview)。</span><span class="sxs-lookup"><span data-stu-id="282d0-111">[Enable managed service identities](https://docs.microsoft.com/azure/active-directory/managed-service-identity/overview).</span></span>
> * <span data-ttu-id="282d0-112">Web アプリケーションに必要なアクセス許可を付与して、キー コンテナーからデータを読み取ります。</span><span class="sxs-lookup"><span data-stu-id="282d0-112">Grant the required permissions for the web application to read data from Key vault.</span></span>

<span data-ttu-id="282d0-113">先に進む前に、[基本的な概念](https://docs.microsoft.com/azure/key-vault/key-vault-whatis#basic-concepts)を理解しておいてください。</span><span class="sxs-lookup"><span data-stu-id="282d0-113">Before you proceed make sure that you are familiar with the [basic concepts](https://docs.microsoft.com/azure/key-vault/key-vault-whatis#basic-concepts).</span></span>

>[!NOTE]
<span data-ttu-id="282d0-114">下記のチュートリアルがベスト プラクティスである理由を理解するには、いくつかの概念を理解する必要があります。</span><span class="sxs-lookup"><span data-stu-id="282d0-114">To understand why the below tutorial is the best practice we need to understand a few concepts.</span></span> <span data-ttu-id="282d0-115">Key Vault は、プログラムでシークレットを格納できる中央リポジトリです。</span><span class="sxs-lookup"><span data-stu-id="282d0-115">Key Vault is a central repository to store secrets programmatically.</span></span> <span data-ttu-id="282d0-116">しかしこれを実行するには、アプリケーション/ユーザーが最初に Key Vault に対する認証を行う (シークレットを提示する) 必要があります。</span><span class="sxs-lookup"><span data-stu-id="282d0-116">But to do so applications / users need to first authenticate to Key Vault i.e. present a secret.</span></span> <span data-ttu-id="282d0-117">セキュリティのベスト プラクティスに従うために、最初のシークレットのローテーションが定期的に行われる必要もあります。</span><span class="sxs-lookup"><span data-stu-id="282d0-117">To follow security best practices this first secret needs to be rotated periodically as well.</span></span> <span data-ttu-id="282d0-118">しかし、Azure で実行される[マネージド サービス ID](https://docs.microsoft.com/azure/active-directory/managed-service-identity/overview) アプリケーションでは、Azure によって自動で管理される ID が提供されます。</span><span class="sxs-lookup"><span data-stu-id="282d0-118">But with [Managed Service Identity](https://docs.microsoft.com/azure/active-directory/managed-service-identity/overview) applications that run in Azure are given an identity which is automatically managed by Azure.</span></span> <span data-ttu-id="282d0-119">これにより、**シークレット導入問題**が解決されます。ユーザー/アプリケーションはベスト プラクティスに従うことができ、最初のシークレットのローテーションについて心配する必要がありません</span><span class="sxs-lookup"><span data-stu-id="282d0-119">This helps solve the **Secret Introduction Problem** where users / applications can follow best practices and not have to worry about rotating the first secret</span></span>

## <a name="prerequisites"></a><span data-ttu-id="282d0-120">前提条件</span><span class="sxs-lookup"><span data-stu-id="282d0-120">Prerequisites</span></span>

<span data-ttu-id="282d0-121">::: zone pivot="nodejs"</span><span class="sxs-lookup"><span data-stu-id="282d0-121">::: zone pivot="nodejs"</span></span>
* <span data-ttu-id="282d0-122">[Node JS](https://nodejs.org/en/) ::: zone-end</span><span class="sxs-lookup"><span data-stu-id="282d0-122">[Node JS](https://nodejs.org/en/) ::: zone-end</span></span>

<span data-ttu-id="282d0-123">::: zone pivot="dotnet, windows"</span><span class="sxs-lookup"><span data-stu-id="282d0-123">::: zone pivot="dotnet, windows"</span></span>
* <span data-ttu-id="282d0-124">次のワークロードでは [Visual Studio 2017 バージョン 15.7.3 以降](https://www.microsoft.com/net/download/windows)。</span><span class="sxs-lookup"><span data-stu-id="282d0-124">[Visual Studio 2017 version 15.7.3 or later](https://www.microsoft.com/net/download/windows) with the following workloads:</span></span>
  * <span data-ttu-id="282d0-125">ASP.NET および Web の開発</span><span class="sxs-lookup"><span data-stu-id="282d0-125">ASP.NET and web development</span></span>
  * <span data-ttu-id="282d0-126">.NET Core クロスプラットフォームの開発</span><span class="sxs-lookup"><span data-stu-id="282d0-126">.NET Core cross-platform development</span></span>
* <span data-ttu-id="282d0-127">[.NET Core 2.1 SDK 以降](https://www.microsoft.com/net/download/windows) :::zone-end</span><span class="sxs-lookup"><span data-stu-id="282d0-127">[.NET Core 2.1 SDK or later](https://www.microsoft.com/net/download/windows) :::zone-end</span></span>

<span data-ttu-id="282d0-128">::: zone pivot="dotnet, mac"</span><span class="sxs-lookup"><span data-stu-id="282d0-128">::: zone pivot="dotnet, mac"</span></span>
* <span data-ttu-id="282d0-129">[Visual Studio for Mac の新機能](https://visualstudio.microsoft.com/vs/mac/)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="282d0-129">See [What’s New in Visual Studio for Mac](https://visualstudio.microsoft.com/vs/mac/).</span></span>
<span data-ttu-id="282d0-130">:::zone-end</span><span class="sxs-lookup"><span data-stu-id="282d0-130">:::zone-end</span></span>

* <span data-ttu-id="282d0-131">Git ([ダウンロード](https://git-scm.com/downloads))。</span><span class="sxs-lookup"><span data-stu-id="282d0-131">Git ([download](https://git-scm.com/downloads)).</span></span>
* <span data-ttu-id="282d0-132">Azure サブスクリプション。</span><span class="sxs-lookup"><span data-stu-id="282d0-132">An Azure subscription.</span></span> <span data-ttu-id="282d0-133">Azure サブスクリプションをお持ちでない場合は、開始する前に[無料アカウント](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)を作成してください。</span><span class="sxs-lookup"><span data-stu-id="282d0-133">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>
* <span data-ttu-id="282d0-134">[Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) バージョン 2.0.4 以降。</span><span class="sxs-lookup"><span data-stu-id="282d0-134">[Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) version 2.0.4 or later.</span></span> <span data-ttu-id="282d0-135">これは、Windows、Mac、Linux に対応しています。</span><span class="sxs-lookup"><span data-stu-id="282d0-135">This is available for Windows, Mac, and Linux.</span></span>

## <a name="login-to-azure"></a><span data-ttu-id="282d0-136">Azure にログインする</span><span class="sxs-lookup"><span data-stu-id="282d0-136">Login to Azure</span></span>

<span data-ttu-id="282d0-137">CLI を使用して Azure にログインするには、次のように入力します。</span><span class="sxs-lookup"><span data-stu-id="282d0-137">To log in to Azure using the CLI, you can type:</span></span>

```azurecli
az login
```

## <a name="create-resource-group"></a><span data-ttu-id="282d0-138">リソース グループを作成する</span><span class="sxs-lookup"><span data-stu-id="282d0-138">Create resource group</span></span>

<span data-ttu-id="282d0-139">[az group create](/cli/azure/group#az-group-create) コマンドでリソース グループを作成します。</span><span class="sxs-lookup"><span data-stu-id="282d0-139">Create a resource group with the [az group create](/cli/azure/group#az-group-create) command.</span></span> <span data-ttu-id="282d0-140">Azure リソース グループとは、Azure リソースのデプロイと管理に使用する論理コンテナーです。</span><span class="sxs-lookup"><span data-stu-id="282d0-140">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="282d0-141">リソース グループ名を選択し、プレース ホルダーを入力してください。</span><span class="sxs-lookup"><span data-stu-id="282d0-141">Please select a Resource Group name and fill in the placeholder.</span></span>
<span data-ttu-id="282d0-142">次の例では、*<YourResourceGroupName>* という名前のリソース グループを *eastus* の場所に作成します。</span><span class="sxs-lookup"><span data-stu-id="282d0-142">The following example creates a resource group named *<YourResourceGroupName>* in the *eastus* location.</span></span>

```azurecli
# To list locations: az account list-locations --output table
az group create --name "<YourResourceGroupName>" --location "East US"
```

<span data-ttu-id="282d0-143">作成したリソース グループは、このチュートリアルの全体を通して使用します。</span><span class="sxs-lookup"><span data-stu-id="282d0-143">The resource group you just created is used throughout this tutorial.</span></span>

## <a name="create-an-azure-key-vault"></a><span data-ttu-id="282d0-144">Azure Key Vault を作成する</span><span class="sxs-lookup"><span data-stu-id="282d0-144">Create an Azure Key Vault</span></span>

<span data-ttu-id="282d0-145">次に、前の手順で作成したリソース グループを使って Key Vault を作成します。</span><span class="sxs-lookup"><span data-stu-id="282d0-145">Next you create a Key Vault using the resource group created in the previous step.</span></span> <span data-ttu-id="282d0-146">この記事全体で Key Vault の名前として "ContosoKeyVault" を使用していますが、一意の名前を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="282d0-146">Although “ContosoKeyVault” is used as the name for the Key Vault throughout this article, you have to use a unique name.</span></span> <span data-ttu-id="282d0-147">次の情報を指定します。</span><span class="sxs-lookup"><span data-stu-id="282d0-147">Provide the following information:</span></span>

* <span data-ttu-id="282d0-148">Key Vault 名 - **こちらで Key Vault 名を選択してください**。</span><span class="sxs-lookup"><span data-stu-id="282d0-148">Vault name - **Select a Key Vault Name here**.</span></span>
* <span data-ttu-id="282d0-149">リソース グループ名 -**こちらでリソース グループ名を選択してください**。</span><span class="sxs-lookup"><span data-stu-id="282d0-149">Resource group name - **Select a Resource Group Name here**.</span></span>
* <span data-ttu-id="282d0-150">場所: **米国東部**。</span><span class="sxs-lookup"><span data-stu-id="282d0-150">The location - **East US**.</span></span>

```azurecli
az keyvault create --name "<YourKeyVaultName>" --resource-group "<YourResourceGroupName>" --location "East US"
```

<span data-ttu-id="282d0-151">この時点で、自分の Azure アカウントが唯一、この新しいコンテナーで任意の操作を実行することを許可されています。</span><span class="sxs-lookup"><span data-stu-id="282d0-151">At this point, your Azure account is the only one authorized to perform any operations on this new vault.</span></span>

## <a name="add-a-secret-to-key-vault"></a><span data-ttu-id="282d0-152">キー コンテナーにシークレットを追加する</span><span class="sxs-lookup"><span data-stu-id="282d0-152">Add a secret to key vault</span></span>

<span data-ttu-id="282d0-153">シークレットのしくみをよく理解できるように、シークレットを追加します。</span><span class="sxs-lookup"><span data-stu-id="282d0-153">We're adding a secret to help illustrate how this works.</span></span> <span data-ttu-id="282d0-154">SQL 接続文字列やその他の情報を機密として保持する必要があるのに、アプリケーションで使用可能になるように保管している場合があります。</span><span class="sxs-lookup"><span data-stu-id="282d0-154">You could be storing a SQL connection string or any other information that you need to keep securely but make available to your application.</span></span> <span data-ttu-id="282d0-155">このチュートリアルでは、パスワードを **AppSecret** と呼び、このパスワード内に **MySecret** という値を格納します。</span><span class="sxs-lookup"><span data-stu-id="282d0-155">In this tutorial, the password will be called **AppSecret** and will store the value of **MySecret** in it.</span></span>

<span data-ttu-id="282d0-156">次のコマンドを入力して、値 **MySecret** を保存する **AppSecret** というシークレットをキー コンテナーに作成します。</span><span class="sxs-lookup"><span data-stu-id="282d0-156">Type the commands below to create a secret in Key Vault called **AppSecret** that will store the value **MySecret**:</span></span>

```azurecli
az keyvault secret set --vault-name "<YourKeyVaultName>" --name "AppSecret" --value "MySecret"
```

<span data-ttu-id="282d0-157">シークレットに格納されている値をプレーンテキストとして表示するには:</span><span class="sxs-lookup"><span data-stu-id="282d0-157">To view the value contained in the secret as plain text:</span></span>

```azurecli
az keyvault secret show --name "AppSecret" --vault-name "<YourKeyVaultName>"
```

<span data-ttu-id="282d0-158">このコマンドは、URI を含むシークレットの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="282d0-158">This command shows the secret information including the URI.</span></span> <span data-ttu-id="282d0-159">これらの手順を完了すると、Azure Key Vault のシークレットへの URI がわかります。</span><span class="sxs-lookup"><span data-stu-id="282d0-159">After completing these steps, you should have a URI to a secret in an Azure Key Vault.</span></span> <span data-ttu-id="282d0-160">この情報を書き留めておいてください。</span><span class="sxs-lookup"><span data-stu-id="282d0-160">Write this information down.</span></span> <span data-ttu-id="282d0-161">後の手順で必要になります。</span><span class="sxs-lookup"><span data-stu-id="282d0-161">You need it in a later step.</span></span>

## <a name="clone-the-repo"></a><span data-ttu-id="282d0-162">リポジトリを複製する</span><span class="sxs-lookup"><span data-stu-id="282d0-162">Clone the Repo</span></span>

<span data-ttu-id="282d0-163">次のコマンドを実行してリポジトリを複製し、ソースを編集するためのローカル コピーを作成します。</span><span class="sxs-lookup"><span data-stu-id="282d0-163">Clone the repo in order to make a local copy for you to edit the source by running the following command:</span></span>

```bash
git clone https://github.com/Azure-Samples/key-vault-node-quickstart.git
```

<span data-ttu-id="282d0-164">::: zone pivot="nodejs"</span><span class="sxs-lookup"><span data-stu-id="282d0-164">::: zone pivot="nodejs"</span></span>

## <a name="install-dependencies"></a><span data-ttu-id="282d0-165">依存関係をインストールする</span><span class="sxs-lookup"><span data-stu-id="282d0-165">Install dependencies</span></span>

<span data-ttu-id="282d0-166">ここで依存関係をインストールします。</span><span class="sxs-lookup"><span data-stu-id="282d0-166">Here we install the dependencies.</span></span> <span data-ttu-id="282d0-167">コマンド cd key-vault-node-quickstart npm install を実行します。</span><span class="sxs-lookup"><span data-stu-id="282d0-167">Run the following commands cd key-vault-node-quickstart npm install</span></span>

<span data-ttu-id="282d0-168">このプロジェクトでは、次の 2 つのノード モジュールを使用しました。</span><span class="sxs-lookup"><span data-stu-id="282d0-168">This project used 2 node modules:</span></span>

* [<span data-ttu-id="282d0-169">ms-rest-azure</span><span class="sxs-lookup"><span data-stu-id="282d0-169">ms-rest-azure</span></span>](https://www.npmjs.com/package/ms-rest-azure) 
* [<span data-ttu-id="282d0-170">azure-keyvault</span><span class="sxs-lookup"><span data-stu-id="282d0-170">azure-keyvault</span></span>](https://www.npmjs.com/package/azure-keyvault)

## <a name="publish-the-web-application-to-azure"></a><span data-ttu-id="282d0-171">Azure に Web アプリケーションを発行する</span><span class="sxs-lookup"><span data-stu-id="282d0-171">Publish the web application to Azure</span></span>

<span data-ttu-id="282d0-172">以下に示したいくつかの手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="282d0-172">Below are the few steps we need to do</span></span>

* <span data-ttu-id="282d0-173">1 つ目の手順は、[Azure App Service](https://azure.microsoft.com/services/app-service/) プランの作成です。</span><span class="sxs-lookup"><span data-stu-id="282d0-173">The 1st step is to create a [Azure App Service](https://azure.microsoft.com/services/app-service/) Plan.</span></span> <span data-ttu-id="282d0-174">このプランには複数の Web アプリを格納することができます。</span><span class="sxs-lookup"><span data-stu-id="282d0-174">You can store multiple web apps in this plan.</span></span>

    ```azurecli
    az appservice plan create --name myAppServicePlan --resource-group myResourceGroup
    ```
* <span data-ttu-id="282d0-175">次に、Web アプリを作成します。</span><span class="sxs-lookup"><span data-stu-id="282d0-175">Next we create a web app.</span></span> <span data-ttu-id="282d0-176">次の例では、<app_name> をグローバルに一意のアプリ名に置き換えてください (有効な文字は a-z、0-9、-)。</span><span class="sxs-lookup"><span data-stu-id="282d0-176">In the following example, replace <app_name> with a globally unique app name (valid characters are a-z, 0-9, and -).</span></span> <span data-ttu-id="282d0-177">ランタイムは NODE|6.9 に設定されています。</span><span class="sxs-lookup"><span data-stu-id="282d0-177">The runtime is set to NODE|6.9.</span></span> <span data-ttu-id="282d0-178">サポートされているすべてのランタイムを確認するには、az webapp list-runtimes を実行します。</span><span class="sxs-lookup"><span data-stu-id="282d0-178">To see all supported runtimes, run az webapp list-runtimes</span></span>

    ```azurecli
    az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app_name> --runtime "NODE|6.9" --deployment-local-git
    ```

    <span data-ttu-id="282d0-179">Web アプリが作成されると、Azure CLI によって次の例のような出力が表示されます。</span><span class="sxs-lookup"><span data-stu-id="282d0-179">When the web app has been created, the Azure CLI shows output similar to the following example:</span></span>

    ```json
    {
      "availabilityState": "Normal",
      "clientAffinityEnabled": true,
      "clientCertEnabled": false,
      "cloningInfo": null,
      "containerSize": 0,
      "dailyMemoryTimeQuota": 0,
      "defaultHostName": "<app_name>.azurewebsites.net",
      "enabled": true,
      "deploymentLocalGitUrl": "https://<username>@<app_name>.scm.azurewebsites.net/<app_name>.git"
      < JSON data removed for brevity. >
    }
    ```
    <span data-ttu-id="282d0-180">新しく作成された Web アプリに移動すると、Web アプリが稼働していることがわかります。</span><span class="sxs-lookup"><span data-stu-id="282d0-180">Browse to your newly created web app and you should see a functioning web app.</span></span> <span data-ttu-id="282d0-181"><app_name> は、アプリの一意の名前に置き換えてください。</span><span class="sxs-lookup"><span data-stu-id="282d0-181">Replace <app_name> with a unique app name.</span></span>

    ```text
    http://<app name>.azurewebsites.net
    ```
    <span data-ttu-id="282d0-182">また、上のコマンドを実行すると、ローカル Git から Azure にデプロイすることができる Git 対応のアプリが作成されます。</span><span class="sxs-lookup"><span data-stu-id="282d0-182">The above command also creates a Git-enabled app which allows you to deploy to azure from your local git.</span></span> 
    <span data-ttu-id="282d0-183">ローカル Git は、"https://<username>@<app_name>.scm.azurewebsites.net/<app_name>.git" という URL を使って構成されています。</span><span class="sxs-lookup"><span data-stu-id="282d0-183">Local git is configured with url of 'https://<username>@<app_name>.scm.azurewebsites.net/<app_name>.git'</span></span>

* <span data-ttu-id="282d0-184">デプロイ ユーザーを作成します。前のコマンドが完了したら、ローカル Git リポジトリに Azure リモートを追加できます。</span><span class="sxs-lookup"><span data-stu-id="282d0-184">Create a deployment user After the previous command is completed you can add add an Azure remote to your local Git repository.</span></span> <span data-ttu-id="282d0-185"><url> を、「アプリの Git を有効にする」で取得した Git リモートの URL で置き換えます。</span><span class="sxs-lookup"><span data-stu-id="282d0-185">Replace <url> with the URL of the Git remote that you got from Enable Git for your app.</span></span>

    ```bash
    git remote add azure <url>
    ```
<span data-ttu-id="282d0-186">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="282d0-186">::: zone-end</span></span>

<span data-ttu-id="282d0-187">::: zone pivot="dotnet"</span><span class="sxs-lookup"><span data-stu-id="282d0-187">::: zone pivot="dotnet"</span></span>

## <a name="open-and-edit-the-solution"></a><span data-ttu-id="282d0-188">ソリューションを開いて編集する</span><span class="sxs-lookup"><span data-stu-id="282d0-188">Open and edit the solution</span></span>

<span data-ttu-id="282d0-189">program.cs ファイルを編集し、特定のキー コンテナー名でサンプルを実行します。</span><span class="sxs-lookup"><span data-stu-id="282d0-189">Edit the program.cs file to run the sample with your specific key vault name:</span></span>

1. <span data-ttu-id="282d0-190">フォルダー key-vault-dotnet-core-quickstart を参照します。</span><span class="sxs-lookup"><span data-stu-id="282d0-190">Browse to the folder key-vault-dotnet-core-quickstart.</span></span>
2. <span data-ttu-id="282d0-191">Visual Studio 2017 で、key-vault-dotnet-core-quickstart.sln ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="282d0-191">Open the key-vault-dotnet-core-quickstart.sln file in Visual Studio 2017.</span></span>
3. <span data-ttu-id="282d0-192">Program.cs ファイルを開き、プレースホルダー *YourKeyVaultName* を先ほど作成したキー コンテナーの名前に更新します。</span><span class="sxs-lookup"><span data-stu-id="282d0-192">Open the Program.cs file and update the placeholder *YourKeyVaultName* with the name of your key vault that you created earlier.</span></span>

<span data-ttu-id="282d0-193">このソリューションでは、[AppAuthentication](https://www.nuget.org/packages/Microsoft.Azure.Services.AppAuthentication) ライブラリと [KeyVault](https://www.nuget.org/packages/Microsoft.Azure.KeyVault) NuGet ライブラリが使用されます。</span><span class="sxs-lookup"><span data-stu-id="282d0-193">This solution uses [AppAuthentication](https://www.nuget.org/packages/Microsoft.Azure.Services.AppAuthentication) and [KeyVault](https://www.nuget.org/packages/Microsoft.Azure.KeyVault) NuGet libraries.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="282d0-194">アプリを実行する</span><span class="sxs-lookup"><span data-stu-id="282d0-194">Run the app</span></span>

<span data-ttu-id="282d0-195">Visual Studio 2017 のメイン メニューで、**[デバッグ]** > **[デバッグなしで開始]** と選択します。</span><span class="sxs-lookup"><span data-stu-id="282d0-195">From the main menu of Visual Studio 2017, select **Debug** > **Start** without debugging.</span></span> <span data-ttu-id="282d0-196">ブラウザーが表示されたら、**[バージョン情報]** ページに移動します。</span><span class="sxs-lookup"><span data-stu-id="282d0-196">When the browser appears, go to the **About** page.</span></span> <span data-ttu-id="282d0-197">**AppSecret** の値が表示されます。</span><span class="sxs-lookup"><span data-stu-id="282d0-197">The value for **AppSecret** is displayed.</span></span>

## <a name="publish-the-web-application-to-azure"></a><span data-ttu-id="282d0-198">Azure に Web アプリケーションを発行する</span><span class="sxs-lookup"><span data-stu-id="282d0-198">Publish the web application to Azure</span></span>

<span data-ttu-id="282d0-199">このアプリを Azure に発行し、Web アプリとしてライブであることと、シークレット値を取得することを確認します。</span><span class="sxs-lookup"><span data-stu-id="282d0-199">Publish this app to Azure to see it live as a web app, and to see that you can fetch the secret value:</span></span>

1. <span data-ttu-id="282d0-200">Visual Studio で、**key-vault-dotnet-core-quickstart** プロジェクトを選択します。</span><span class="sxs-lookup"><span data-stu-id="282d0-200">In Visual Studio, select the **key-vault-dotnet-core-quickstart** project.</span></span>
2. <span data-ttu-id="282d0-201">**[発行]** > **[開始]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="282d0-201">Select **Publish** > **Start**.</span></span>
3. <span data-ttu-id="282d0-202">新しい **App Service** を作成し、**[発行]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="282d0-202">Create a new **App Service**, and then select **Publish**.</span></span>
4. <span data-ttu-id="282d0-203">アプリ名を **keyvaultdotnetcorequickstart** に変更します。</span><span class="sxs-lookup"><span data-stu-id="282d0-203">Change the app name to **keyvaultdotnetcorequickstart**.</span></span>
5. <span data-ttu-id="282d0-204">**[作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="282d0-204">Select **Create**.</span></span>

>[!VIDEO https://sec.ch9.ms/ch9/e93d/a6ac417f-2e63-4125-a37a-8f34bf0fe93d/KeyVault_high.mp4]

<span data-ttu-id="282d0-205">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="282d0-205">::: zone-end</span></span>

## <a name="enable-managed-service-identities"></a><span data-ttu-id="282d0-206">マネージド サービス ID を有効にする</span><span class="sxs-lookup"><span data-stu-id="282d0-206">Enable managed service identities</span></span>

<span data-ttu-id="282d0-207">Azure Key Vault は、資格情報およびその他のキーやシークレットを安全に保管する方法を提供しますが、コードは Azure Key Vault に認証してそれらを取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="282d0-207">Azure Key Vault provides a way to securely store credentials and other keys and secrets, but your code needs to authenticate to Azure Key Vault to retrieve them.</span></span> <span data-ttu-id="282d0-208">マネージド サービス ID は、Azure Active Directory (Azure AD) で自動的に管理されている ID を Azure サービスに付与することで、これを簡単にします。</span><span class="sxs-lookup"><span data-stu-id="282d0-208">Managed Service Identity makes this easier by giving Azure services an automatically managed identity in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="282d0-209">この ID を使用して、コードに資格情報が含まれていなくても、Key Vault を含む Azure AD の認証をサポートする任意のサービスに認証することができます。</span><span class="sxs-lookup"><span data-stu-id="282d0-209">You can use this identity to authenticate to any service that supports Azure AD authentication, including Key Vault, without having any credentials in your code.</span></span>

1. <span data-ttu-id="282d0-210">Azure CLI に戻ります。</span><span class="sxs-lookup"><span data-stu-id="282d0-210">Return to the Azure CLI.</span></span>
2. <span data-ttu-id="282d0-211">assign-identity コマンドを実行して、このアプリケーションの ID を作成します。</span><span class="sxs-lookup"><span data-stu-id="282d0-211">Run the assign-identity command to create the identity for this application:</span></span>

   ```azurecli
   az webapp identity assign --name "keyvaultdotnetcorequickstart" --resource-group "<YourResourceGroupName>"
   ```

>[!NOTE]
><span data-ttu-id="282d0-212">このプロシージャのコマンドは、ポータルに移動して、Web アプリケーション プロパティの **[マネージド サービス ID]** を **[オン]** に切り替えることと同等です。</span><span class="sxs-lookup"><span data-stu-id="282d0-212">The command in this procedure is the equivalent of going to the portal and switching **Managed service identity** to **On** in the web application properties.</span></span>

## <a name="assign-permissions-to-your-application-to-read-secrets-from-key-vault"></a><span data-ttu-id="282d0-213">アプリケーションにアクセス許可を割り当ててキー コンテナーからシークレットを読み取る</span><span class="sxs-lookup"><span data-stu-id="282d0-213">Assign permissions to your application to read secrets from Key Vault</span></span>

<span data-ttu-id="282d0-214">アプリケーションを Azure に発行するときの出力をメモします。</span><span class="sxs-lookup"><span data-stu-id="282d0-214">Make a note of the output when you publish the application to Azure.</span></span> <span data-ttu-id="282d0-215">次の形式にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="282d0-215">It should be of the format:</span></span>

```json
        {
          "principalId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
          "tenantId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
          "type": "SystemAssigned"
        }
```

<span data-ttu-id="282d0-216">次に、キー コンテナーの名前と **PrincipalId** の値を使用してこのコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="282d0-216">Then, run this command by using the name of your key vault and the value of **PrincipalId**:</span></span>

```azurecli
az keyvault set-policy --name '<YourKeyVaultName>' --object-id <PrincipalId> --secret-permissions get
```

<span data-ttu-id="282d0-217">::: zone pivot="nodejs"</span><span class="sxs-lookup"><span data-stu-id="282d0-217">::: zone pivot="nodejs"</span></span>
## <a name="deploy-the-node-app-to-azure-and-retrieve-the-secret-value"></a><span data-ttu-id="282d0-218">Node アプリを Azure にデプロイしてシークレット値を取得する</span><span class="sxs-lookup"><span data-stu-id="282d0-218">Deploy the Node App to Azure and retrieve the secret value</span></span>

<span data-ttu-id="282d0-219">以上で準備は完了です。</span><span class="sxs-lookup"><span data-stu-id="282d0-219">Now that everything is set.</span></span> <span data-ttu-id="282d0-220">次のコマンドを実行してアプリを Azure にデプロイします。</span><span class="sxs-lookup"><span data-stu-id="282d0-220">Run the following command to deploy the app to Azure</span></span>

```bash
git push azure master
```

<span data-ttu-id="282d0-221">その後ブラウザーで https://<app_name>.azurewebsites.net にアクセスすると、シークレット値が確認できます。</span><span class="sxs-lookup"><span data-stu-id="282d0-221">After this when you browse https://<app_name>.azurewebsites.net you can see the secret value.</span></span>
<span data-ttu-id="282d0-222"><YourKeyVaultName> という名前を実際のコンテナー名に置き換えたことを確認してください。 ::: zone-end</span><span class="sxs-lookup"><span data-stu-id="282d0-222">Make sure that you replaced the name <YourKeyVaultName> with your vault name ::: zone-end</span></span>

<span data-ttu-id="282d0-223">::: zone pivot="dotnet" これで、アプリケーションを実行すると、取得されたシークレットの値が表示されます。</span><span class="sxs-lookup"><span data-stu-id="282d0-223">::: zone pivot="dotnet" Now when you run the application, you should see your secret value retrieved.</span></span>
<span data-ttu-id="282d0-224">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="282d0-224">::: zone-end</span></span>

## <a name="next-steps"></a><span data-ttu-id="282d0-225">次のステップ</span><span class="sxs-lookup"><span data-stu-id="282d0-225">Next steps</span></span>

<span data-ttu-id="282d0-226">::: zone pivot="nodejs"</span><span class="sxs-lookup"><span data-stu-id="282d0-226">::: zone pivot="nodejs"</span></span>
* [<span data-ttu-id="282d0-227">Azure Key Vault のホーム ページ</span><span class="sxs-lookup"><span data-stu-id="282d0-227">Azure Key Vault Home Page</span></span>](https://azure.microsoft.com/services/key-vault/)
* [<span data-ttu-id="282d0-228">Azure Key Vault のドキュメント</span><span class="sxs-lookup"><span data-stu-id="282d0-228">Azure Key Vault Documentation</span></span>](https://docs.microsoft.com/azure/key-vault/)
* [<span data-ttu-id="282d0-229">Azure SDK For Node</span><span class="sxs-lookup"><span data-stu-id="282d0-229">Azure SDK For Node</span></span>](https://docs.microsoft.com/javascript/api/overview/azure/key-vault)
* <span data-ttu-id="282d0-230">[Azure REST API リファレンス](https://docs.microsoft.com/rest/api/keyvault/) ::: zone-end</span><span class="sxs-lookup"><span data-stu-id="282d0-230">[Azure REST API Reference](https://docs.microsoft.com/rest/api/keyvault/) ::: zone-end</span></span>

<span data-ttu-id="282d0-231">::: zone pivot="dotnet"</span><span class="sxs-lookup"><span data-stu-id="282d0-231">::: zone pivot="dotnet"</span></span>
* [<span data-ttu-id="282d0-232">Azure Key Vault のホーム ページ</span><span class="sxs-lookup"><span data-stu-id="282d0-232">Azure Key Vault home page</span></span>](https://azure.microsoft.com/services/key-vault/)
* [<span data-ttu-id="282d0-233">Azure Key Vault のドキュメント</span><span class="sxs-lookup"><span data-stu-id="282d0-233">Azure Key Vault documentation</span></span>](https://docs.microsoft.com/azure/key-vault/)
* [<span data-ttu-id="282d0-234">Azure SDK for .NET</span><span class="sxs-lookup"><span data-stu-id="282d0-234">Azure SDK For .NET</span></span>](https://github.com/Azure/azure-sdk-for-net)
* <span data-ttu-id="282d0-235">[Azure REST API リファレンス](https://docs.microsoft.com/rest/api/keyvault/) ::: zone-end</span><span class="sxs-lookup"><span data-stu-id="282d0-235">[Azure REST API reference](https://docs.microsoft.com/rest/api/keyvault/) ::: zone-end</span></span>