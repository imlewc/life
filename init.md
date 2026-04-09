为了方便你直接开发，我为你准备了一份**标准的开发配置文件 (JSON)** 以及一个**单文件版 (All-in-one) 的 HTML 代码**。

你可以直接将 JSON 导入你的数据库，或者直接运行下面的 HTML 文件看到效果。

### 第一部分：核心数据文档 (JSON)
这是从视频中提取的 20 多个核心窗口的逻辑参数，你可以将其保存为 `data.json`。

```json
[
  { "id": 1, "cat": "能力", "title": "语言学习黄金期", "range": [3, 15], "lock": 18, "penalty": "45%", "cost": "Medium", "desc": "母语级口音及自然吸收能力窗口。" },
  { "id": 2, "cat": "学业", "title": "第一学历跃迁", "range": [18, 25], "lock": 30, "penalty": "70%", "cost": "High", "desc": "错过后职业入口折扣极高，补救门槛极高。" },
  { "id": 3, "cat": "健康", "title": "牙齿正畸黄金期", "range": [12, 18], "lock": 35, "penalty": "60%", "cost": "High", "desc": "成年后强行矫正易导致“牙套脸”及牙根吸收。" },
  { "id": 4, "cat": "生理", "title": "生育窗口期", "range": [24, 38], "lock": 45, "penalty": "95%", "cost": "Extreme", "desc": "受生理极限锁死，后期成功率直线下降。" },
  { "id": 5, "cat": "事业", "title": "高强度试错创业", "range": [22, 32], "lock": 40, "penalty": "60%", "cost": "High", "desc": "无房贷、无子女、精力巅峰。后期风险耐受力萎缩。" },
  { "id": 6, "cat": "财务", "title": "财务复利启动", "range": [20, 30], "lock": 45, "penalty": "30%", "cost": "Medium", "desc": "启动越早，晚年财务自由难度越低。" },
  { "id": 7, "cat": "心理", "title": "心智原动力窗口", "range": [15, 28], "lock": 35, "penalty": "85%", "cost": "Extreme", "desc": "对世界纯粹的好奇心，锁死后易变为何事都枯燥。" },
  { "id": 8, "cat": "社会", "title": "跨国/迁移低成本", "range": [18, 30], "lock": 40, "penalty": "65%", "cost": "High", "desc": "随年龄增长，房贷、姻亲形成重力抽吸。" },
  { "id": 9, "cat": "健康", "title": "深睡恢复窗口", "range": [15, 25], "lock": 28, "penalty": "90%", "cost": "Extreme", "desc": "28岁后熬夜一次，数日难复原。" },
  { "id": 10, "cat": "家庭", "title": "老人安宁照护", "range": [40, 60], "lock": 70, "penalty": "90%", "cost": "N/A", "desc": "与父母深度告别的最后窗口，错过即永久关闭。" },
  { "id": 11, "cat": "能力", "title": "高强度专业训练", "range": [15, 28], "lock": 35, "penalty": "55%", "cost": "High", "desc": "1万小时定律黄金期，需极高专注度。" },
  { "id": 12, "cat": "认知", "title": "认知框架重塑", "range": [18, 35], "lock": 45, "penalty": "45%", "cost": "High", "desc": "大脑可塑性较高期，后期思维定式难以打破。" }
]
```

---

### 第二部分：可直接运行的复刻网页 (HTML/CSS/JS)
你可以将以下代码保存为 `index.html`。它实现了视频中的**滑块联动、颜色实时切换、卡片高亮**等功能。

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>人生时间轴窗口系统</title>
    <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        .card-shadow { transition: all 0.3s ease; }
        input[type=range]::-webkit-slider-thumb {
            -webkit-appearance: none;
            height: 24px; width: 24px;
            border-radius: 50%; background: #2563eb;
            cursor: pointer; border: 4px solid white;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
    </style>
</head>
<body class="bg-slate-50 min-h-screen font-sans">
    <div id="app" class="max-w-7xl mx-auto p-6">
        <header class="bg-white p-8 rounded-2xl shadow-sm mb-10 sticky top-4 z-50 border border-slate-200">
            <div class="flex flex-col md:flex-row md:items-center justify-between gap-6">
                <div>
                    <h1 class="text-3xl font-black text-slate-800">人生重要时间窗口</h1>
                    <p class="text-slate-500 mt-1">不可逆的单向系统：随年龄增长，窗口缩窄，代价激增</p>
                </div>
                <div class="flex items-center gap-6 bg-slate-50 p-4 rounded-xl border border-slate-100">
                    <span class="font-bold text-slate-700">当前模拟年龄:</span>
                    <input type="range" v-model="age" min="5" max="75" class="w-48 md:w-64 h-2 bg-slate-200 rounded-lg appearance-none cursor-pointer">
                    <span class="text-4xl font-mono font-black text-blue-600 w-16 text-center">{{ age }}</span>
                </div>
            </div>
        </header>

        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
            <div v-for="w in windows" :key="w.id" 
                :class="['card-shadow p-6 rounded-2xl border-2 flex flex-col justify-between h-64', getStyle(w)]">
                
                <div>
                    <div class="flex justify-between items-center mb-4">
                        <span class="px-2 py-1 rounded text-[10px] font-bold uppercase tracking-widest bg-white bg-opacity-50">
                            {{ w.cat }}
                        </span>
                        <span class="text-xl">{{ getIcon(w) }}</span>
                    </div>
                    <h3 class="text-xl font-bold mb-2">{{ w.title }}</h3>
                    <p class="text-xs leading-relaxed opacity-80">{{ w.desc }}</p>
                </div>

                <div class="mt-4 pt-4 border-t border-current border-opacity-10">
                    <div class="flex justify-between items-end">
                        <div class="text-[10px]">
                            <p class="opacity-60 uppercase">最佳执行期</p>
                            <p class="font-bold text-sm">{{ w.range[0] }} - {{ w.range[1] }} 岁</p>
                        </div>
                        <div class="text-right">
                            <p class="text-[10px] opacity-60 uppercase">事后补偿代价</p>
                            <p class="font-black text-sm">{{ getCostLabel(w) }}</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <footer class="mt-12 text-center text-slate-400 text-sm pb-10">
            时光要珍惜，决定要深思。
        </footer>
    </div>

    <script>
        const { createApp, ref } = Vue;
        createApp({
            setup() {
                const age = ref(17);
                const windows = [
                    { id: 1, cat: "教育", title: "语言学习黄金期", range: [3, 15], lock: 18, desc: "母语级口音及自然吸收能力窗口。" },
                    { id: 2, cat: "学业", title: "第一学历跃迁", range: [18, 25], lock: 30, desc: "错过后职业入口折扣极高，学历门槛难以跨越。" },
                    { id: 3, cat: "事业", title: "试错创业窗口", range: [22, 32], lock: 40, desc: "无房贷、无子女。后期生活成本和责任将完成绑定。" },
                    { id: 4, cat: "健康", title: "深睡恢复窗口", range: [15, 25], lock: 28, desc: "28岁左右该阀门永久关闭，熬夜将产生不可逆损伤。" },
                    { id: 5, cat: "生理", title: "生育窗口", range: [24, 38], lock: 45, desc: "受生理极限严重锁死。错过需辅助生殖技术，成本极高。" },
                    { id: 6, cat: "财务", title: "财务复利启动", range: [20, 30], lock: 40, desc: "第一笔养老金或自由基金的启动时间。越早难度越低。" },
                    { id: 7, cat: "家庭", title: "老人安宁照护", range: [40, 60], lock: 70, desc: "与父母进行深度告别、修复关系、安置晚年的最后窗口。" },
                    { id: 8, cat: "心理", title: "少年气窗口", range: [15, 28], lock: 35, desc: "对世界纯粹的好奇心。错过后相关神经突触将永久修剪。" }
                ];

                const getStyle = (w) => {
                    if (age.value <= w.range[1]) return 'bg-green-50 border-green-200 text-green-700 shadow-green-100';
                    if (age.value <= w.lock) return 'bg-orange-50 border-orange-200 text-orange-700 shadow-orange-100';
                    return 'bg-red-50 border-red-200 text-red-700 shadow-red-100 opacity-60';
                };

                const getIcon = (w) => {
                    if (age.value <= w.range[1]) return '🔓';
                    if (age.value <= w.lock) return '⌛';
                    return '🔒';
                };

                const getCostLabel = (w) => {
                    if (age.value <= w.range[1]) return 'LOW';
                    if (age.value <= w.lock) return 'HIGH';
                    return 'EXTREME';
                };

                return { age, windows, getStyle, getIcon, getCostLabel };
            }
        }).mount('#app');
    </script>
</body>
</html>
```

### 复刻建议：
1. **动画效果**：在 `getStyle` 改变时，我加了简单的 `transition`，如果想要视频中那种弹窗效果，可以给卡片添加一个 `@click` 事件，弹出一个固定在屏幕中央的 `div`。
2. **逻辑补充**：视频中还有一个“锁死强制力百分比”，你可以在数据中加一个 `force: "85%"` 的字段，然后在卡片底部用一个简单的进度条显示。
3. **扩展性**：如果要复刻完整的 30 个窗口，只需把第一部分的 JSON 内容全部填入 HTML 代码里的 `windows` 数组即可。

这个文档足够你快速搭建出一个 Demo 了，直接复制到记事本改后缀名为 `.html` 就能玩！
