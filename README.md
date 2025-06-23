# 个人在线图床 (My Image Hosting)

这是一个轻量级、易于部署的个人图床解决方案，基于 Node.js 和 Express 构建。您可以将它一键部署到 Vercel，并使用 Cloudinary 作为免费、可靠的图片存储后端。

## ✨ 核心功能

- **一键部署**: 使用 Vercel 按钮，只需几分钟即可拥有自己的在线图床。
- **云端存储**: 所有图片上传至 Cloudinary，享受其稳定、快速的全球 CDN 服务。
- **简洁界面**: 提供一个干净、直观的网页上传界面。
- **完全免费**: 本项目所使用的核心服务 (Vercel, Cloudinary) 均提供慷慨的免费套餐。
- **高度可定制**: 完整的源代码，方便您根据自己的需求进行修改和扩展。

## 🛠️ 准备工作

在开始部署之前，请确保您已拥有以下平台的账号：

- **[GitHub](https://github.com/)**: 用于克隆本项目和管理代码。
- **[Vercel](https://vercel.com/)**: 用于托管和部署应用（可使用 GitHub 账号直接登录）。
- **[Cloudinary](https://cloudinary.com/)**: 用于存储图片，您需要从其仪表板获取 `Cloud Name`, `API Key`, 和 `API Secret`。

准备好这些，将使您的部署过程更加顺畅。

## 🚀 一键部署 (推荐)

如果您不想关心技术细节，只想快速拥有一个自己的图床，请使用以下“一键部署”按钮。点击后，您将被引导至 Vercel，它会自动帮您完成所有设置。

**部署前，请确保您已经注册了 [Cloudinary](https://cloudinary.com/) 账号，并准备好了您的 `Cloud Name`, `API Key`, 和 `API Secret`。**

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https%3A%2F%2Fgithub.com%2Fczjainiaini%2Fmy-image-hosting&env=CLOUDINARY_CLOUD_NAME,CLOUDINARY_API_KEY,CLOUDINARY_API_SECRET&envDescription=请输入您的Cloudinary凭据以便上传图片&envLink=https%3A%2F%2Fgithub.com%2Fczjainiaini%2Fmy-image-hosting%234-%25E9%2585%258D%25E7%25BD%25AE-cloudinary-api-%25E5%25AF%2586%25E9%2592%25A5)



---

## 📚 手动分步教程

如果您想了解每个步骤的细节或在本地进行开发，请遵循以下详细教程。


这是一个详细的教程，旨在帮助初学者使用 Node.js、Express、Cloudinary 和 Vercel 从零开始创建一个功能完整的在线图床应用。即使您是编程新手，跟随本教程的步骤，也能成功部署自己的图床服务。

## 功能简介

*   通过网页界面上传图片。
*   图片存储在 Cloudinary 云存储服务中，安全可靠。
*   项目部署在 Vercel 平台上，提供免费的 HTTPS 域名，全球访问速度快。
*   后端使用 Node.js 和 Express 构建，代码简洁易懂。

## 1. 准备工作 (Prerequisites)

在开始之前，请确保您的电脑上安装了以下软件，并注册了所需平台的账号。

*   **[Node.js](https://nodejs.org/)**: JavaScript 运行环境。请下载并安装 LTS (长期支持) 版本。
*   **代码编辑器**: 例如 [Visual Studio Code](https://code.visualstudio.com/) (推荐)，或其他您喜欢的编辑器。
*   **[Git](https://git-scm.com/)**: 版本控制工具，用于将代码上传到 GitHub。
*   **[GitHub](https://github.com/) 账号**: 用于托管您的项目代码。
*   **[Cloudinary](https://cloudinary.com/) 账号**: 用于存储上传的图片。注册免费套餐即可满足本项目需求。
*   **[Vercel](https://vercel.com/) 账号**: 用于部署和托管您的网站。可以使用 GitHub 账号直接登录。

## 2. 项目初始化与文件创建

首先，我们需要在本地电脑上创建项目文件夹和所有必需的文件。

### 2.1 创建项目目录

在您喜欢的位置创建一个名为 `image-hosting` 的文件夹，这将是我们的项目根目录。

### 2.2 初始化 Node.js 项目

1.  打开您的代码编辑器 (如 VS Code)，然后通过 `文件 > 打开文件夹` 打开刚刚创建的 `image-hosting` 目录。
2.  在 VS Code 中，按下 `Ctrl + `` ` (反引号键，通常在键盘左上角) 打开集成终端。
3.  在终端中输入以下命令并按回车，以初始化一个新的 Node.js 项目：

    ```bash
    npm init -y
    ```

    这个命令会创建一个 `package.json` 文件，它记录了项目的基本信息和依赖项。

### 2.3 安装项目依赖

我们需要安装几个 Node.js 包来帮助我们构建应用。在终端中运行以下命令：

```bash
npm install express multer cloudinary dotenv cors
```

*   `express`: 一个流行的 Node.js Web 应用框架。
*   `multer`: 用于处理 `multipart/form-data` 类型的表单数据，主要用于文件上传。
*   `cloudinary`: Cloudinary 官方提供的 Node.js SDK，方便我们与 Cloudinary API 交互。
*   `dotenv`: 用于从 `.env` 文件中加载环境变量，保护我们的敏感信息。
*   `cors`: 用于处理跨域资源共享 (CORS) 问题。

### 2.4 创建项目文件结构

现在，让我们创建项目所需的所有文件和文件夹。您可以在 VS Code 的文件浏览器中右键点击来创建文件和文件夹。

最终的项目结构应该如下所示：

```
image-hosting/
├── node_modules/      (自动生成)
├── public/
│   └── index.html
├── .gitignore
├── package.json
├── package-lock.json  (自动生成)
├── server.js
└── vercel.json
```

**请手动创建以下文件和文件夹：**

1.  创建一个名为 `public` 的文件夹。
2.  在 `public` 文件夹内，创建一个 `index.html` 文件。
3.  在项目根目录 (`image-hosting/`) 下，创建 `server.js`, `.gitignore`, 和 `vercel.json` 文件。

## 3. 编写代码

接下来，我们将填充这些文件的内容。

### 3.1 `public/index.html` (前端页面)

这是用户将看到的网页界面。将以下代码复制到 `public/index.html` 文件中：

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>图片上传</title>
    <style>
        body { font-family: Arial, sans-serif; display: flex; justify-content: center; align-items: center; height: 100vh; background-color: #f4f4f9; margin: 0; }
        .container { background: white; padding: 2rem; border-radius: 8px; box-shadow: 0 4px 6px rgba(0,0,0,0.1); text-align: center; }
        input[type="file"] { margin-bottom: 1rem; }
        button { padding: 0.5rem 1rem; background-color: #007bff; color: white; border: none; border-radius: 4px; cursor: pointer; }
        button:hover { background-color: #0056b3; }
        #result { margin-top: 1rem; }
        #imageUrl { width: 100%; padding: 0.5rem; margin-top: 0.5rem; box-sizing: border-box; }
    </style>
</head>
<body>
    <div class="container">
        <h1>上传图片到图床</h1>
        <input type="file" id="imageFile" accept="image/*">
        <button onclick="uploadImage()">上传</button>
        <div id="result"></div>
    </div>

    <script>
        async function uploadImage() {
            const fileInput = document.getElementById('imageFile');
            const resultDiv = document.getElementById('result');

            if (fileInput.files.length === 0) {
                resultDiv.innerHTML = '请先选择一个图片文件！';
                return;
            }

            const file = fileInput.files[0];
            const formData = new FormData();
            formData.append('image', file);

            resultDiv.innerHTML = '正在上传...';

            try {
                const response = await fetch('/upload', {
                    method: 'POST',
                    body: formData
                });

                const data = await response.json();

                if (response.ok) {
                    resultDiv.innerHTML = `
                        <p>上传成功！</p>
                        <p>图片 URL:</p>
                        <input id="imageUrl" type="text" value="${data.url}" readonly onclick="this.select();">
                    `;
                } else {
                    throw new Error(data.message || '上传失败');
                }
            } catch (error) {
                resultDiv.innerHTML = `上传出错: ${error.message}`;
            }
        }
    </script>
</body>
</html>
```

### 3.2 `server.js` (后端服务器)

这是我们应用的核心，处理文件上传逻辑。将以下代码复制到 `server.js` 文件中：

```javascript
require('dotenv').config();
const express = require('express');
const multer = require('multer');
const cloudinary = require('cloudinary').v2;
const cors = require('cors');
const path = require('path');

// 检查环境变量
if (!process.env.CLOUDINARY_CLOUD_NAME || !process.env.CLOUDINARY_API_KEY || !process.env.CLOUDINARY_API_SECRET) {
    console.error('错误: Cloudinary 环境变量未设置. 请在 .env 文件或部署平台中设置 CLOUDINARY_CLOUD_NAME, CLOUDINARY_API_KEY, 和 CLOUDINARY_API_SECRET.');
    process.exit(1);
}

// 配置 Cloudinary
cloudinary.config({
    cloud_name: process.env.CLOUDINARY_CLOUD_NAME,
    api_key: process.env.CLOUDINARY_API_KEY,
    api_secret: process.env.CLOUDINARY_API_SECRET
});

const app = express();
const port = process.env.PORT || 3000;

// 使用 CORS 中间件
app.use(cors());

// 配置 Multer 进行内存存储
const storage = multer.memoryStorage();
const upload = multer({ storage: storage });

// 静态文件服务，用于提供 public 文件夹中的内容
app.use(express.static(path.join(__dirname, 'public')));

// 根路径路由，发送 index.html
app.get('/', (req, res) => {
    res.sendFile(path.join(__dirname, 'public', 'index.html'));
});

// 文件上传路由
app.post('/upload', upload.single('image'), async (req, res) => {
    if (!req.file) {
        return res.status(400).json({ message: '未选择文件' });
    }

    try {
        const result = await new Promise((resolve, reject) => {
            const uploadStream = cloudinary.uploader.upload_stream(
                { resource_type: 'auto' },
                (error, result) => {
                    if (error) reject(error);
                    else resolve(result);
                }
            );
            uploadStream.end(req.file.buffer);
        });
        res.json({ url: result.secure_url });
    } catch (error) {
        console.error('Cloudinary 上传错误:', error);
        res.status(500).json({ message: '上传到 Cloudinary 失败' });
    }
});

app.listen(port, () => {
    console.log(`服务器运行在 http://localhost:${port}`);
});
```

### 3.3 `.gitignore` (忽略文件)

这个文件告诉 Git 哪些文件或文件夹不应该被上传到 GitHub 仓库。这对于避免上传敏感信息（如 API 密钥）和不必要的文件（如 `node_modules`）至关重要。

将以下内容复制到 `.gitignore` 文件中：

```
# 依赖文件夹
node_modules

# 环境变量文件
.env

# 日志文件
npm-debug.log*
yarn-debug.log*
yarn-error.log*

# 构建输出
dist
build
```

### 3.4 `vercel.json` (Vercel 部署配置)

这个文件告诉 Vercel 如何构建和部署我们的项目。

将以下内容复制到 `vercel.json` 文件中：

```json
{
    "version": 2,
    "builds": [
        {
            "src": "server.js",
            "use": "@vercel/node"
        }
    ],
    "routes": [
        {
            "src": "/(.*)",
            "dest": "server.js"
        }
    ]
}
```

## 4. 配置 Cloudinary API 密钥

为了让我们的应用能够将图片上传到 Cloudinary，我们需要获取 API 密钥并安全地配置它们。

1.  **登录 Cloudinary**: 访问您的 [Cloudinary Dashboard](https://cloudinary.com/console)。
2.  **找到密钥**: 在仪表板首页，您会找到 `Cloud Name`, `API Key`, 和 `API Secret`。点击 `API Secret` 旁边的眼睛图标可以显示它。
3.  **创建 `.env` 文件**: 在项目的根目录 (`image-hosting/`) 下创建一个名为 `.env` 的新文件。**这个文件非常重要，且不应该被上传到 GitHub。**
4.  **添加密钥到 `.env` 文件**: 将您的 Cloudinary 凭据复制到 `.env` 文件中，格式如下：

    ```
    CLOUDINARY_CLOUD_NAME=<Your-Cloudinary-Cloud-Name>
    CLOUDINARY_API_KEY=<Your-Cloudinary-API-Key>
    CLOUDINARY_API_SECRET=<Your-Cloudinary-API-Secret>
    ```

    请将 `你的...` 替换为您自己的实际凭据。

## 5. 本地运行和测试

在部署到互联网之前，先在本地测试以确保一切正常。

1.  在 VS Code 的终端中，运行以下命令启动服务器：

    ```bash
    node server.js
    ```

2.  如果一切顺利，您会看到 `服务器运行在 http://localhost:3000` 的消息。
3.  打开您的浏览器，访问 `http://localhost:3000`。
4.  您应该能看到上传界面。尝试选择一张图片并点击“上传”按钮，如果配置正确，您将看到上传成功的提示和图片的 URL。

## 6. 部署到 Vercel

现在，是时候将我们的图床应用发布到互联网上了！

### 6.1 上传代码到 GitHub

1.  **创建 GitHub 仓库**: 登录 GitHub，创建一个新的空仓库 (repository)，例如命名为 `my-image-hosting`。
2.  **初始化本地 Git 仓库**: 回到 VS Code 的终端，按 `Ctrl + C` 停止正在运行的本地服务器。然后依次运行以下命令，将您的代码与远程 GitHub 仓库关联并上传。

    ```bash
    git init
    git add .
    git commit -m "Initial commit"
    git branch -M main
    git remote add origin https://github.com/<Your-GitHub-Username>/<Your-Repository-Name>.git
    git push -u origin main
    ```

    **注意**: 请将 `你的用户名` 和 `你的仓库名` 替换为您自己的 GitHub 用户名和仓库名。

### 6.2 在 Vercel 上部署

1.  **登录 Vercel**: 使用您的 GitHub 账号登录 [Vercel](https://vercel.com/)。
2.  **导入项目**: 在 Vercel 的仪表板 (Dashboard) 上，点击 `Add New...` -> `Project`。
3.  **选择 GitHub 仓库**: Vercel 会显示您的 GitHub 仓库列表。找到并选择您刚刚创建的 `my-image-hosting` 仓库，然后点击 `Import`。
4.  **配置环境变量**: 这是最关键的一步！在配置项目页面，展开 `Environment Variables` (环境变量) 部分。在这里，您需要添加在本地 `.env` 文件中使用的三个 Cloudinary 密钥：
    *   `CLOUDINARY_CLOUD_NAME`
    *   `CLOUDINARY_API_KEY`
    *   `CLOUDINARY_API_SECRET`

    一个一个地添加，将您在 Cloudinary 仪表板上找到的值粘贴进去。

5.  **部署**: 添加完环境变量后，直接点击 `Deploy` 按钮。Vercel 会自动拉取您的代码，安装依赖，并根据 `vercel.json` 的配置进行构建和部署。

## 7. 访问和使用

部署过程通常需要一两分钟。完成后，Vercel 会为您生成一个公开的网址 (例如 `my-image-hosting.vercel.app`)。点击这个网址，您就可以在任何地方访问和使用您的个人图床了！

恭喜您！您已经成功搭建并部署了一个属于自己的在线图床应用。
