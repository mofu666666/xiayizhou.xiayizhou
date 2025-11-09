<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
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
        }

        /* 单个提示窗口样式 */
        #single-tip {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 350px;
            height: 120px;
            background: pink;
            border-radius: 10px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
            padding: 20px;
            z-index: 1000;
            border: 3px solid white;
        }

        .single-tip-text {
            font-size: 16px;
            font-weight: bold;
            color: #333;
            line-height: 1.5;
        }

        /* 批量提示窗口样式 */
        .batch-tip {
            position: fixed;
            width: 350px;
            height: 120px;
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
            padding: 15px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
            border: 2px solid white;
            cursor: pointer;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            z-index: 999;
        }

        .batch-tip:hover {
            transform: scale(1.05);
            box-shadow: 0 8px 25px rgba(0,0,0,0.3);
        }

        .batch-tip-text {
            font-size: 14px;
            font-weight: bold;
            color: #333;
            line-height: 1.4;
        }

        /* 控制按钮 */
        .control-panel {
            position: fixed;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            z-index: 1001;
            display: flex;
            gap: 10px;
        }

        .control-btn {
            padding: 10px 20px;
            background: rgba(255,255,255,0.9);
            border: none;
            border-radius: 20px;
            font-family: 'Microsoft YaHei';
            font-size: 14px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
        }

        .control-btn:hover {
            background: white;
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(0,0,0,0.3);
        }

        /* 提示信息 */
        .hint {
            position: fixed;
            top: 20px;
            left: 50%;
            transform: translateX(-50%);
            background: rgba(255,255,255,0.9);
            padding: 10px 20px;
            border-radius: 20px;
            font-size: 12px;
            z-index: 1001;
        }
    </style>
</head>
<body>
    <div id="single-tip">
        <div class="single-tip-text">妹妹,我叫夏以昼，是你的哥哥</div>
    </div>

    <div class="control-panel">
        <button class="control-btn" onclick="startBatchTips()">开始批量提示</button>
        <button class="control-btn" onclick="clearAllTips()">清空所有提示 (空格键)</button>
    </div>

    <div class="hint">关闭第一个窗口或点击按钮开始批量显示温馨提醒</div>

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

        // 背景颜色数组
        const bgColors = [
            'lightblue', 'lightgreen', 'lightyellow', 'pink', 'lavender',
            'lightcyan', 'lightcoral', 'wheat', 'thistle', 'azure',
            'palegoldenrod', 'mistyrose', 'aliceblue', 'honeydew', 'lavenderblush'
        ];

        let batchWindows = [];
        let singleTipWindow = document.getElementById('single-tip');

        // 初始化事件监听
        function init() {
            // 单个提示窗口点击事件
            singleTipWindow.addEventListener('click', startBatchTips);
            
            // 空格键全局事件
            document.addEventListener('keydown', function(event) {
                if (event.code === 'Space') {
                    clearAllTips();
                }
            });
        }

        // 开始批量提示
        function startBatchTips() {
            // 隐藏单个提示窗口
            singleTipWindow.style.display = 'none';
            
            // 创建批量提示窗口
            createBatchWindows(20);
        }

        // 创建批量窗口
        function createBatchWindows(count) {
            if (count <= 0) return;

            const windowElement = document.createElement('div');
            windowElement.className = 'batch-tip';
            
            // 随机位置
            const screenWidth = window.innerWidth;
            const screenHeight = window.innerHeight;
            const x = Math.random() * (screenWidth - 350);
            const y = Math.random() * (screenHeight - 120);
            
            // 随机提示和背景色
            const randomTip = tips[Math.floor(Math.random() * tips.length)];
            const randomBg = bgColors[Math.floor(Math.random() * bgColors.length)];
            
            windowElement.style.left = x + 'px';
            windowElement.style.top = y + 'px';
            windowElement.style.background = randomBg;
            
            windowElement.innerHTML = `<div class="batch-tip-text">${randomTip}</div>`;
            
            // 点击窗口可关闭
            windowElement.addEventListener('click', function() {
                this.remove();
                batchWindows = batchWindows.filter(w => w !== this);
            });
            
            document.body.appendChild(windowElement);
            batchWindows.push(windowElement);
            
            // 递归创建下一个窗口
            setTimeout(() => {
                createBatchWindows(count - 1);
            }, 50);
        }

        // 清空所有提示
        function clearAllTips() {
            // 移除批量窗口
            batchWindows.forEach(window => {
                if (window.parentNode) {
                    window.parentNode.removeChild(window);
                }
            });
            batchWindows = [];
            
            // 显示单个提示窗口
            singleTipWindow.style.display = 'flex';
        }

        // 页面加载完成后初始化
        window.addEventListener('DOMContentLoaded', init);
    </script>
</body>
</html>
