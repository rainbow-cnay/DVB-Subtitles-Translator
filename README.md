# DVBTrans - MPEGTS 流字幕翻译工具

## 简介
DVBTrans 是一个专门用于处理 MPEGTS 流中字幕的自动翻译工具。它能够实时处理输入的 TS 流，并输出带有翻译字幕的新 TS 流。支持从网络 HTTP 流或本地文件读取 TS 流，并可以输出为 HTTP 服务或新的 TS 文件。

## 主要功能
- 实时字幕翻译：支持多种语言之间的字幕翻译
- 文件转换：将本地 TS 文件转换为带翻译字幕的新文件
- 网络代理：提供 HTTP 服务，支持实时流媒体翻译
- 系统托盘：支持最小化到系统托盘运行

## 系统要求
- Windows 操作系统 （32位/64位）
- 网络连接（用于网络代理功能和翻译服务）
- 足够的磁盘空间（用于文件转换功能）
- 安装tesseract OCR 4.x 软件，并安装所需的语言支持

## 节目来源
- 存储MPEGTS流的TS文件
- TS流媒体，可来自OPENATV、OPENPLI等类似的DVB-S/S2、DVB-T/T2接收机的节目流

## 翻译功能依赖项
- 使用OPENAI API，需要APIKEY
- 使用GOOGLE GEMINI 2.0 FLASH(LITE) API, 需要APIKEY
- 自建本地大模型完成翻译

## 播放器
- 电脑上，Windows下可用POTPLAYER、MPC-HC、VLC PLAYER等，LINUX下可用OPEN_TV、YUKI-IPTV等
- 安卓系统，建议 IPTV 或 IPTV PRO

## 使用说明

### 1. 文件转换模式
1. 启动程序
2. 在 "Language Settings" 区域：
   - 选择源语言（原始字幕语言）
   - 选择目标语言（需要翻译成的语言）
3. 在文件转换区域：
   - 点击 "Browse..." 选择源 TS 文件
   - 点击目标文件的 "Browse..." 选择保存位置
   - 点击 "Start File Conversion" 开始转换
   - 可随时点击 "Stop File Conversion" 停止转换

### 2. 网络代理模式
1. 启动程序
2. 在 "Language Settings" 区域设置语言
3. 点击 "Start HTTP Server" 启动代理服务器（默认端口：8888）
4. 使用媒体播放器访问 `http://localhost:8888` 观看带翻译字幕的流
5. 点击 "Stop HTTP Server" 停止服务

### 3. 系统托盘功能
- 程序可以最小化到系统托盘运行
- 双击托盘图标：恢复主窗口
- 右键托盘图标：
  - Show Window：显示主窗口
  - Exit：退出程序

## 技术架构

### 核心组件
- `MainForm.pas/dfm`：主窗体和用户界面实现
- `TSProcessor.pas`：MPEGTS 流处理核心
- `Trans.pas`：基于 OpenAI API 的文本翻译模块
- `DVBSubUnit.pas`：字幕图像解码和转换
- `OCRUnit.pas`：图像文字识别
- `GolombBuffer.pas`：数据缓冲区处理

### 工作流程
1. 读取并解析 TS 流数据包
2. 提取 PAT 表获取 PMT PID
3. 解析 PMT 表获取字幕流 PID
4. 修改 PMT 表添加新字幕流
5. 处理字幕流：
   - 提取字幕图像
   - OCR 转换为文本
   - 翻译文本
   - 生成新字幕流
6. 输出处理后的 TS 流

## 注意事项
- 确保网络连接稳定，特别是在使用网络代理模式时
- 文件转换模式下，请确保有足够的磁盘空间
- 翻译质量取决于 OCR 识别准确度和翻译服务的性能
- 建议在使用前先进行小规模测试

## 开发信息
- 开发环境：Delphi 12 IDE
- 网络组件：使用 Delphi 自带的 Indy 网络组件
- 支持多客户端并发访问
- 支持多节目源同时处理

## 许可证
[待补充]

## 联系方式
[待补充]
