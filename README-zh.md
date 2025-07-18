# docsify-to-pdf

[English](README.md) | [中文](README-zh.md)

> docsify-to-pdf 远端库版本，已经不兼容了，请使用本地库版本。

## 本地库版本使用

### 1.构建 link

将当前代码下载到本地，然后安装依赖。

```sh
# 下载代码
git clone https://github.com/ningg/docsify-to-pdf.git
cd docsify-to-pdf
# 安装依赖
npm install
# 构建 link
npm link
```

### 2.使用 link

在希望使用 docsify-to-pdf 的其他项目中（比如：`/path/to/your/other/project`），执行：

```sh
cd /path/to/your/other/project
npm link docsify-to-pdf
```

并且在目录中，添加 `.docsifytopdfrc.js` 文件，内容如下：

```js
module.exports = {
    // 必需：指定目录文件路径数组
    contents: ["_sidebar.md"],
    
    // 必需：PDF 输出路径
    pathToPublic: "pdf/LLM_30_Essential_Lectures_AI.pdf",
    
    // 可选：PDF 选项（Puppeteer 配置）
    // https://pptr.dev/api/puppeteer.pdfoptions
    pdfOptions: {
      format: "A4",
      margin: {
        top: "20mm",
        right: "20mm",
        bottom: "20mm",
        left: "20mm"
      },
      printBackground: true,
      displayHeaderFooter: true,
      headerTemplate: '<span>title</span>',  
      footerTemplate: '<div style="font-size: 10px; text-align: center; width: 100%;">第 <span class="pageNumber"></span> 页，共 <span class="totalPages"></span> 页</div>'
    },

    // 必填：Chrome 浏览器可执行文件路径
    chromeExecutablePath: "/Applications/Google Chrome.app/Contents/MacOS/Google Chrome",
    
    // 可选：是否删除临时文件
    removeTemp: true,
    
    // 可选：媒体类型模拟（print 或 screen）
    // https://pptr.dev/api/puppeteer.page.emulatemediatype
    emulateMedia: "screen",
    
    // 可选：静态文件路径
    pathToStatic: "static",
    
    // 可选：主 Markdown 文件名
    mainMdFilename: "README.md",
    
    // 可选：docsify 入口点路径
    pathToDocsifyEntryPoint: ".",
    
    // 可选：分页符配置
    pageBreak: {
      // 是否启用分页符
      enabled: true,
      // 分页符样式：'div' 或 'css'
      type: 'div',
      // 自定义分页符 HTML（当 type 为 'div' 时使用）
      html: '<div style="page-break-after: always;"></div>',
      // 自定义 CSS 样式（当 type 为 'css' 时使用）
      css: `
        .markdown-section h1, .markdown-section h2, .markdown-section h3 {
          page-break-before: always;
        }
        .markdown-section h1:first-child, .markdown-section h2:first-child, .markdown-section h3:first-child {
          page-break-before: avoid;
        }
        .markdown-section {
          page-break-inside: avoid;
        }
        .markdown-section h1, .markdown-section h2, .markdown-section h3 {
          break-before: page;
        }
        .markdown-section h1:first-child, .markdown-section h2:first-child, .markdown-section h3:first-child {
          break-before: avoid;
        }
      `
    }
  };
```


再在目录下的 `package.json` 中，添加脚本：

```json
{
    "scripts": {
      "convert": "node_modules/.bin/docsify-to-pdf"
    }
}
```

最后，当前目录下，执行：

```sh
npm run convert
```

