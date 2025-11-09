<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>温馨提醒</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Microsoft YaHei', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            overflow: hidden;
            touch-action: manipulation;
            -webkit-tap-highlight-color: transparent;
        }

        /* 单个提示窗口样式 */
        #single-tip {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 180px;
            height: 140px;
            background: #f0f0f0;
            border: 1px solid #0078d7;
            box-shadow: 0 4px 8px rgba(0,0,0,0.3);
            z-index: 1000;
            overflow: hidden;
            cursor: pointer;
        }

        .window-titlebar {
            height: 22px;
            background: linear-gradient(180deg, #0078d7, #005a9e);
            color: white;
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 0 8px;
            font-size: 11px;
            font-weight: bold;
            border-bottom: 1px solid #005a9e;
        }

        .window-title {
            font-weight: bold;
        }

        .window-controls {
            display: flex;
            gap: 6px;
        }

        .window-control {
            width: 10px;
            height: 10px;
            border: 1px solid rgba(255,255,255,0.3);
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 8px;
            font-weight: bold;
            color: rgba(0,0,0,0.6);
        }

        .control-close { 
            background: #ff5f57; 
            border-color: #e0443e;
        }
        .control-min { 
            background: #ffbd2e; 
            border-color: #e0a323;
        }
        .control-max { 
            background: #28ca42; 
            border-color: #1dad34;
        }

        .window-content {
            height: calc(100% - 22px);
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
            padding: 12px;
            background: #f0f0f0;
        }

        .single-tip-text {
            font-size: 12px;
            font-weight: bold;
            color: #000;
            line-height: 1.3;
        }

        /* 批量提示窗口样式 */
        .batch-tip {
            position: fixed;
            width: 150px;
            height: 110px;
            border: 1px solid #ccc;
            box-shadow: 0 2px 6px rgba(0,0,0,0.2);
            cursor: pointer;
            z-index: 999;
            overflow: hidden;
            opacity: 0;
            transform: scale(0.8);
            animation: popIn 0.5s cubic-bezier(0.25, 0.46, 0.45, 0.94) forwards;
            background: #f0f0f0;
        }

        @keyframes popIn {
            0% {
                opacity: 0;
                transform: scale(0.8) translateY(15px);
            }
            70% {
                opacity: 1;
                transform: scale(1.02);
            }
            100% {
                opacity: 1;
                transform: scale(1);
            }
        }

        .batch-tip.fade-out {
            animation: fadeOut 0.4s ease forwards;
        }

        @keyframes fadeOut {
            to {
                opacity: 0;
                transform: scale(0.4) rotate(360deg);
            }
        }

        .batch-titlebar {
            height: 18px;
            background: linear-gradient(180deg, #0078d7, #005a9e);
            color: white;
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 0 6px;
            font-size: 9px;
            font-weight: bold;
            border-bottom: 1px solid #005a9e;
        }

        .batch-content {
            height: calc(100% - 18px);
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
            padding: 8px;
            background: #f0f0f0;
        }

        .batch-tip-text {
            font-size: 10px;
            font-weight: bold;
            color: #000;
            line-height: 1.2;
            word-wrap: break-word;
        }

        /* 控制按钮 */
        .control-panel {
            position: fixed;
            bottom: 15px;
            left: 50%;
            transform: translateX(-50%);
            z-index: 1001;
            display: flex;
            gap: 8px;
            flex-wrap: wrap;
            justify-content: center;
            padding: 0 10px;
            width: 100%;
        }

        .control-btn {
            padding: 6px 12px;
            background: #e1e1e1;
            border: 1px solid #adadad;
            border-radius: 3px;
            font-family: 'Microsoft YaHei';
            font-size: 11px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.2s ease;
            box-shadow: 0 1px 2px rgba(0,0,0,0.1);
            min-width: 80px;
            touch-action: manipulation;
        }

        .control-btn:hover {
            background: #d5d5d5;
            border-color: #0078d7;
        }

        .control-btn:active {
            background: #c9c9c9;
        }

        /* 提示信息 */
        .hint {
            position: fixed;
            top: 10px;
            left: 50%;
            transform: translateX(-50%);
            background: rgba(255,255,255,0.9);
            padding: 6px 12px;
            border-radius: 3px;
            font-size: 9px;
            z-index: 1001;
            text-align: center;
            max-width: 90vw;
            box-shadow: 0 1px 3px rgba(0,0,0,0.1);
            border: 1px solid #ccc;
        }

        /* 进度条 */
        .progress {
            position: fixed;
            top: 40px;
            left: 50%;
            transform: translateX(-50%);
            width: 120px;
            height: 4px;
            background: rgba(255,255,255,0.3);
            border-radius: 2px;
            z-index: 1001;
            display: none;
            border: 1px solid #ccc;
        }

        .progress-bar {
            height: 100%;
            background: linear-gradient(90deg, #0078d7, #005a9e);
            border-radius: 2px;
            width: 0%;
            transition: width 0.2s ease;
        }

        /* 手机特定样式 */
        @media (max-width: 768px) {
            #single-tip {
                width: 160px;
                height: 120px;
            }
            
            .single-tip-text {
                font-size: 11px;
            }
            
            .batch-tip {
                width: 140px;
                height: 100px;
            }
            
            .batch-tip-text {
                font-size: 9px;
            }
            
            .control-btn {
                padding: 5px 10px;
                font-size: 10px;
                min-width: 70px;
            }
            
            .hint {
                font-size: 8px;
                padding: 5px 10px;
            }
        }

        /* 防止文本选择 */
        .batch-tip, #single-tip, .control-btn {
            -webkit-user-select: none;
            -moz-user-select: none;
            -ms-user-select: none;
            user-select: none;
        }
    </style>
</head>
<body>
    <div id="single-tip">
        <div class="window-titlebar">
            <div class="window-title">专属提醒</div>
            <div class="window-controls">
                <div class="window-control control-close"></div>
                <div class="window-control control-min"></div>
                <div class="window-control control-max"></div>
            </div>
        </div>
        <div class="window-content">
            <div class="single-tip-text">妹妹,我叫夏以昼，是你的哥哥</div>
        </div>
    </div>

    <div class="control-panel">
        <button class="control-btn" onclick="startSequentialTips()">开始逐个弹出</button>
        <button class="control-btn" onclick="clearAllTips()">清空所有提示</button>
    </div>

    <div class="hint">点击第一个窗口开始逐个弹出100个温馨提醒<br>点击单个提示窗口可关闭</div>

    <div class="progress" id="progress">
        <div class="progress-bar" id="progressBar"></div>
    </div>

    <script>
        // 提示语数组
        const tips = [
            '我恰好也比你想象中的多爱你一点',
            '请唤醒我',
            '你已经很让我骄傲了',
            '等你睡醒，一切都来得及',
            '因为我是哥哥，哥哥就是愿意替妹妹死的',
            '我一直在这里，从来没有被分走过',
            '和好券的有限期是永远',
            '骗你是小狗，不是夏以昼',
            '你愿意给的，就是我想要的',
            '你想得到的，就是我愿意付出的',
            '如果这是感受你的代价，那我接受',
            '你也有一点罪好不好，别让我太孤独了',
            '你第一次拉住我的手的那一天，我就已经跑不掉了',
            '我想要你留在这里，留下来，跟我过一百年',
            '我一直想和你在同一边的世界',
            '你一定要做世界上最快乐的人',
            '即使是疼痛，只要来源于你，我就想要',
            '我可不是什么越喜欢就越克制的人',
            '我们以后没有分别，只有团圆',
            '我们回家',
            '哥哥在',
        ];

        // 背景颜色数组 - 使用Windows经典颜色
        const bgColors = [
            '#f0f8ff', '#f5f5f5', '#fff8dc', '#ffe4e1', '#e6e6fa',
            '#f0ffff', '#ffe4e1', '#f5deb3', '#d8bfd8', '#f0f0f0',
            '#eef5ee', '#fdf5e6', '#faf0e6', '#fffaf0', '#f8f8ff',
            '#f5fffa', '#fafad2', '#fffacd', '#f0fff0', '#fff0f5'
        ];

        let batchWindows = [];
        let singleTipWindow = document.getElementById('single-tip');
        let progressElement = document.getElementById('progress');
        let progressBar = document.getElementById('progressBar');
        let isCreating = false;
        let creationInterval;

        // 初始化事件监听
        function init() {
            // 单个提示窗口点击事件
            singleTipWindow.addEventListener('click', startSequentialTips);
            
            // 空格键全局事件
            document.addEventListener('keydown', function(event) {
                if (event.code === 'Space') {
                    clearAllTips();
                }
            });

            // 触摸事件优化
            document.addEventListener('touchstart', function() {}, { passive: true });
        }

        // 开始逐个弹出提示
        function startSequentialTips() {
            if (isCreating) return;
            
            // 隐藏单个提示窗口
            singleTipWindow.style.display = 'none';
            
            // 显示进度条
            progressElement.style.display = 'block';
            progressBar.style.width = '0%';
            
            isCreating = true;
            let createdCount = 0;
            const totalCount = 100;
            
            // 清除现有窗口
            clearAllTips();
            
            // 逐个创建窗口
            creationInterval = setInterval(() => {
                if (createdCount >= totalCount) {
                    clearInterval(creationInterval);
                    isCreating = false;
                    progressElement.style.display = 'none';
                    return;
                }
                
                createSingleWindow();
                createdCount++;
                
                // 更新进度条
                progressBar.style.width = `${(createdCount / totalCount) * 100}%`;
            }, 120); // 每120毫秒创建一个新窗口
        }

        // 创建单个窗口
        function createSingleWindow() {
            const windowElement = document.createElement('div');
            windowElement.className = 'batch-tip';
            
            // 随机位置 - 允许触碰屏幕边缘
            const screenWidth = window.innerWidth;
            const screenHeight = window.innerHeight;
            const windowWidth = 150;
            const windowHeight = 110;
            
            // 允许窗口紧贴屏幕边缘
            const x = Math.random() * (screenWidth - windowWidth);
            const y = Math.random() * (screenHeight - windowHeight);
            
            // 随机提示和背景色
            const randomTip = tips[Math.floor(Math.random() * tips.length)];
            const randomBg = bgColors[Math.floor(Math.random() * bgColors.length)];
            
            windowElement.style.left = x + 'px';
            windowElement.style.top = y + 'px';
            windowElement.style.background = randomBg;
            windowElement.style.zIndex = 1000 + batchWindows.length;
            
            // 窗口结构 - 删除"温馨提示"字样
            windowElement.innerHTML = `
                <div class="batch-titlebar">
                    <div class="window-title">提示</div>
                    <div class="window-controls">
                        <div class="window-control control-close"></div>
                    </div>
                </div>
                <div class="batch-content">
                    <div class="batch-tip-text">${randomTip}</div>
                </div>
            `;
            
            // 点击窗口可关闭单个窗口
            windowElement.addEventListener('click', function() {
                this.classList.add('fade-out');
                setTimeout(() => {
                    if (this.parentNode) {
                        this.parentNode.removeChild(this);
                    }
                    batchWindows = batchWindows.filter(w => w !== this);
                }, 400);
            });

            // 添加触摸反馈
            windowElement.addEventListener('touchstart', function() {
                this.style.transform = 'scale(0.95)';
            });

            windowElement.addEventListener('touchend', function() {
                this.style.transform = 'scale(1)';
            });
            
            document.body.appendChild(windowElement);
            batchWindows.push(windowElement);
        }

        // 清空所有提示
        function clearAllTips() {
            // 停止创建过程
            if (creationInterval) {
                clearInterval(creationInterval);
                isCreating = false;
            }
            
            progressElement.style.display = 'none';
            
            // 添加清除动画
            batchWindows.forEach((window, index) => {
                setTimeout(() => {
                    window.classList.add('fade-out');
                    setTimeout(() => {
                        if (window.parentNode) {
                            window.parentNode.removeChild(window);
                        }
                    }, 400);
                }, index * 15);
            });
            
            // 清空数组
            batchWindows = [];
            
            // 显示单个提示窗口
            setTimeout(() => {
                singleTipWindow.style.display = 'block';
                singleTipWindow.style.animation = 'popIn 0.5s ease-out';
            }, 200);
        }

        // 防止滚动
        document.addEventListener('touchmove', function(e) {
            if (batchWindows.length > 0) {
                e.preventDefault();
            }
        }, { passive: false });

        // 页面加载完成后初始化
        window.addEventListener('DOMContentLoaded', init);
        
        // 防止页面缩放
        document.addEventListener('gesturestart', function(e) {
            e.preventDefault();
        });
    </script>
</body>
</html>
