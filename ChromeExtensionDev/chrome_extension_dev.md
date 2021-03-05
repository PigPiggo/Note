# 起步
扩展是由不同的组件构成的；组件包括background_scripts, content_scripts, 和一个options_page, UI_elements以及其他的业务代码文件. 扩展的组件是由HTML, css, 和JS等前端技术开发. 扩展组件可以没有option也能有对应的功能
> An extension's components will depend on its functionality and may not require every option)
# 深入概念
## manifest.json
`icons`: 
  - 128必须要(安装和chrome网上应用商店中都要使用), 
  - 48的在管理页面中使用
  - 16的作为favicon
  - 最好用png
`chrmoe.browserAction`: 
  - 浏览器工具栏上必有扩展图标, 还可以有工具提示(tooltips), 徽章(badge)和弹出框(popup)
  - Tooltip:
    - 可以通过`manifest.json`中的`browser_action.default_title`设置, 也可以调用`browserAction.setTitle`方法
  - Badge
    - 最多4个字符
    - `browserAction.setBadgeText` 设置文本
    - `browserAction.setBadgeBackgroundColor` 设置颜色
- commands
  - 自定义快捷键, 但是不会覆盖浏览器默认快捷键
  - 在background.js中监听
  ```javascript
  chrome.commands.onCommand.addListener(function(command) {
    console.log('Command:', command);
  });
  ```
  - 快捷键
    - 全局作用域: 默认当chrome聚焦的时候, 快捷键才会生效
    - 仅将Ctrl + Shift + [0..9]指定为全局快捷键
    - `global: true`
- content_scripts
  - 运行在浏览器页面上下文, 可以访问DOM(`document.getElementById ()`)
  - 