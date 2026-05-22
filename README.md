# 摇摇吃
  
    基于微信小程序的餐厅随机推荐应用。获取用户定位，通过摇一摇/转盘互动随机推荐附近餐厅，解决"到了饭点不知道吃什么"
      的选择困难症。
  ## 功能
    - **定位获取** —进入小程序自动获取用户定位（降级到默认城市广州）
    - **筛选条件** —距离范围 / 菜系类型 / 价格区间（均可选，非必选）
    - **摇一摇互动** —点击"开摇"触发转盘动画，1.5s 后展示推荐结果
    - **推荐结果** —餐厅名称、封面图、评分、人均价格、距离、地址、精选评论
    - **一键导航** —跳转微信地图发起导航
    - **换一家** —重新随机推荐（已推荐过的不会重复出现）
  ## 技术栈
    | 项 | 选择 |
    |---|------|
    | 框架 | 微信小程序原生 |
    | 地图 API | 高德地图 Web API |
    | 测试 | Jest + miniprogram-simulate |
    | 代码规范 | ESLint + Prettier |
    | 语言 | ES6 |
 ## 项目结构
    ```
    ├── miniprogram/                 # 小程序源码
    │   ├── app.js / app.json / app.wxss   # 入口文件
    │   ├── project.config.json      # 微信开发者工具配置
    │   ├── core/                    # 基础设施
    │   │   ├── constants.js         # 常量定义
    │   │   ├── event.js             # 事件总线
    │   │   └── http.js              # wx.request 封装
    │   ├── models/                  # 数据模型
    │   │   ├── restaurant.js        # 餐厅模型
    │   │   └── filter.js            # 筛选模型
    │   ├── data/                    # 数据访问层
    │   │   ├── amap.js              # 高德 API 封装
    │   │   └── cache.js             # 本地缓存
    │   ├── services/                # 业务服务层
    │   │   ├── location.js          # 定位服务
    │   │   ├── filter.js            # 筛选规则
    │   │   └── recommend.js         # 推荐引擎
    │   ├── components/              # UI 组件
    │   │   ├── filter-bar/          # 筛选栏
    │   │   ├── spin-wheel/          # 转盘
    │   │   └── restaurant-card/     # 餐厅卡片
    │   └── pages/                   # 页面
    │       ├── index/               # 首页
    │       └── result/              # 推荐结果页
                   # npm 配置
   ```
    ## 架构分层
   
    ```
    Pages (UI层)
      └─ Components (组件层)
           └─ Services (业务层)
                └─ Data (数据访问层)
                     └─ Core (基础设施层)
    Models (数据模型) ←被多层使用
    ```
   
    依赖方向：上层依赖下层，下层不感知上层。
   
    ## 快速开始
   
    ### 前置条件
   
    - [微信开发者工具](https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html)
    - Node.js ≥16
    - 高德地图 API Key（[申请地址](https://console.amap.com/dev/key/app)）
   
    ### 配置 API Key
   
    1. 在 `miniprogram/app.js` 中将 `amapKey` 替换为你的高德 API Key：
   
    ```js
    globalData: {
      amapKey: 'YOUR_KEY',  // 替换为你的 Key
    }
    ```
   
    2. 确保高德 API Key 已开通 Web 服务 API 权限。
   
  ### 导入项目
   
    1. 打开微信开发者工具
   2. 选择"导入项目"
   3. 项目目录选择 `miniprogram/`
   4. AppID 使用 `project.config.json` 中的 `wxf17df2e1b0cf619b`（或替换为你自己的）
  
   ### 运行测试
