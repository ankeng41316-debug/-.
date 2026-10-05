<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>專業美甲美睫報價計算機</title>
    <style>
        :root { --primary-color: #ff8fa3; --bg-color: #fff5f6; }
        body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; max-width: 500px; margin: 10px auto; padding: 20px; background-color: var(--bg-color); color: #4a4a4a; }
        .card { background: white; padding: 20px; border-radius: 16px; box-shadow: 0 4px 15px rgba(255,143,163,0.15); }
        h2 { text-align: center; color: #d94e66; margin-top: 0; }
        .section-title { font-weight: bold; margin: 15px 0 8px 0; border-left: 4px solid var(--primary-color); padding-left: 8px; color: #333; }
        .grid-2 { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
        .radio-tile, .check-tile { display: block; border: 2px solid #eee; padding: 10px; border-radius: 10px; text-align: center; cursor: pointer; background: #fafafa; }
        input[type="radio"], input[type="checkbox"] { display: none; }
        input[type="radio"]:checked + .radio-tile, input[type="checkbox"]:checked + .check-tile { background: #ffe3e7; border-color: var(--primary-color); color: #d94e66; font-weight: bold; }
        .flex-row { display: flex; justify-content: space-between; align-items: center; margin-bottom: 10px; background: #fdfdfd; padding: 8px; border-radius: 8px; border: 1px solid #eee; }
        .counter-btn { width: 30px; height: 30px; border: 1px solid #ccc; background: white; border-radius: 5px; font-size: 18px; cursor: pointer; }
        .counter-val { width: 30px; text-align: center; font-weight: bold; display: inline-block; }
        .custom-add-box { display: flex; gap: 5px; margin-top: 15px; }
        .custom-add-box input { padding: 8px; border: 1px solid #ccc; border-radius: 6px; }
        .btn-add { background: var(--primary-color); color: white; border: none; border-radius: 6px; padding: 8px 12px; cursor: pointer; font-weight: bold; }
        .total-box { margin-top: 20px; padding: 15px; background: #ffe3e7; border-radius: 10px; text-align: center; font-size: 1.4em; font-weight: bold; color: #d94e66; border: 2px dashed var(--primary-color); }
        .reset-btn { background: #999; color: white; border: none; width: 100%; padding: 10px; border-radius: 8px; margin-top: 10px; cursor: pointer; font-weight: bold; }
    </style>
</head>
<body>

<div class="card">
    <h2>💅 美甲報價計算機</h2>
    
    <!-- 1. 款式底底價 (單選) -->
    <div class="section-title">✨ 基礎款式底價</div>
    <div class="grid-2">
        <label><input type="radio" name="base" value="400" checked><span class="radio-tile">單色 \$400<br><small>(可跳一色)</small></span></label>
        <label><input type="radio" name="base" value="500"><span class="radio-tile">貓眼 \$500</span></label>
        <label><input type="radio" name="base" value="500"><span class="radio-tile">漸層 \$500</span></label>
    </div>

    <!-- 2. 加配/增值服務 (可複選/單選) -->
    <div class="section-title">加價項目 / 變化</div>
    <div class="flex-row">
        <span>🎨 跳色 (每多1色+40)</span>
        <div>
            <button class="counter-btn" onclick="changeCount('jumpColor', -1)">-</button>
            <span class="counter-val" id="jumpColor">0</span>
            <button class="counter-btn" onclick="changeCount('jumpColor', 1)">+</button>
        </div>
    </div>

    <!-- 3. 指隻計費項目 -->
    <div class="section-title">按隻加資項目</div>
    <div class="flex-row">
        <span>✏️ 手繪 (單隻 \$50)</span>
        <div>
            <button class="counter-btn" onclick="changeCount('art', -1)">-</button>
            <span class="counter-val" id="art">0</span>
            <button class="counter-btn" onclick="changeCount('art', 1)">+</button>
        </div>
    </div>
    <div class="flex-row">
        <span>💎 貼鑽 (單隻 \$50)</span>
        <div>
            <button class="counter-btn" onclick="changeCount('diamond', -1)">-</button>
            <span class="counter-val" id="diamond">0</span>
            <button class="counter-btn" onclick="changeCount('diamond', 1)">+</button>
        </div>
    </div>
    <div class="flex-row">
        <span>🪞 鏡面 (單隻 \$50)</span>
        <div>
            <button class="counter-btn" onclick="changeCount('mirror', -1)">-</button>
            <span class="counter-val" id="mirror">0</span>
            <button class="counter-btn" onclick="changeCount('mirror', 1)">+</button>
        </div>
    </div>

    <!-- 4. 延甲服務 -->
    <div class="section-title">🪵 延甲服務 (單隻)</div>
    <div class="grid-2" style="grid-template-columns: 1fr 1fr;">
        <div class="flex-row" style="margin:0; padding:5px;">
            <span style="font-size:14px;">本店 (\$100)</span>
            <div>
                <button class="counter-btn" onclick="changeCount('extendHome', -1)">-</button>
                <span class="counter-val" id="extendHome">0</span>
                <button class="counter-btn" onclick="changeCount('extendHome', 1)">+</button>
            </div>
        </div>
        <div class="flex-row" style="margin:0; padding:5px;">
            <span style="font-size:14px;">他店 (\$150)</span>
            <div>
                <button class="counter-btn" onclick="changeCount('extendOther', -1)">-</button>
                <span class="counter-val" id="extendOther">0</span>
                <button class="counter-btn" onclick="changeCount('extendOther', 1)">+</button>
            </div>
        </div>
    </div>

    <!-- 5. 動態動態新增的自訂項目列表 -->
    <div class="section-title">➕ 自訂與現場加價</div>
    <div id="customItemsContainer"></div>

    <!-- 新增自訂項目表單 -->
    <div class="custom-add-box">
        <input type="text" id="customName" placeholder="項目名稱(如:造型/大鑽)" style="flex: 2;">
        <input type="number" id="customPrice" placeholder="金額" style="flex: 1;">
        <button class="btn-add" onclick="addCustomItem()">新增</button>
    </div>

    <!-- 6. 總金額計算結算 -->
    <div class="total-box">
        總計金額： NT\$ <span id="totalPrice">400</span> 元
    </div>
    
    <button class="reset-btn" onclick="resetAll()">全部歸零清空</button>
</div>

<script>
    // 數量計數器儲存器
    const counts = { jumpColor: 0, art: 0, diamond: 0, mirror: 0, extendHome: 0, extendOther: 0 };
    // 儲存動態新增的自訂項目
    let customItems = [];

    // 處理數量加減
    function changeCount(key, amount) {
        counts[key] = Math.max(0, counts[key] + amount);
        document.getElementById(key).innerText = counts[key];
        calculateTotal();
    }

    // 動態新增欄位功能
    function addCustomItem() {
        const nameInput = document.getElementById('customName');
        const priceInput = document.getElementById('customPrice');
        const name = nameInput.value.trim();
        const price = parseInt(priceInput.value);

        if (!name || isNaN(price) || price < 0) {
            alert('請輸入正確的項目名稱與金額！');
            return;
        }

        const item = { id: Date.now(), name: name, price: price, count: 1 };
        customItems.push(item);
        
        nameInput.value = '';
        priceInput.value = '';
        renderCustomItems();
        calculateTotal();
    }

    // 刪除自訂項目
    function removeCustomItem(id) {
        customItems = customItems.filter(item => item.id !== id);
        renderCustomItems();
        calculateTotal();
    }

    // 變更自訂項目數量
    function changeCustomCount(id, amount) {
        const item = customItems.find(item => item.id === id);
        if (item) {
            item.count = Math.max(0, item.count + amount);
            if (item.count === 0) {
                removeCustomItem(id);
                return;
            }
            renderCustomItems();
            calculateTotal();
        }
    }

    // 渲染自訂項目到畫面
    function renderCustomItems() {
        const container = document.getElementById('customItemsContainer');
        container.innerHTML = '';
        customItems.forEach(item => {
            const div = document.createElement('div');
            div.className = 'flex-row';
            div.innerHTML = `
                <span>⚙️ ${item.name} ($${item.price})</span>
                <div>
                    <button class="counter-btn" onclick="changeCustomCount(${item.id}, -1)">-</button>
                    <span class="counter-val">${item.count}</span>
                    <button class="counter-btn" onclick="changeCustomCount(${item.id}, 1)">+</button>
                    <button class="counter-btn" style="border:none; color:red; margin-left:10px;" onclick="removeCustomItem(${item.id})">🗑️</button>
                </div>
            `;
            container.appendChild(div);
        });
    }

    // 計算總金額
    function calculateTotal() {
        // 1. 基本底價
        const basePrice = parseInt(document.querySelector('input[name="base"]:checked').value);
        
        // 2. 固定項目金額計算
        let total = basePrice;
        total += counts.jumpColor * 40;
        total += counts.art * 50;
        total += counts.diamond * 50;
        total += counts.mirror * 50;
        total += counts.extendHome * 100;
        total += counts.extendOther * 150;

        // 3. 自訂項目金額計算
        customItems.forEach(item => {
            total += item.price * item.count;
        });

        // 顯示總價
        document.getElementById('totalPrice').innerText = total;
    }

    // 全部重置清空
    function resetAll() {
        Object.keys(counts).forEach(key => { counts[key] = 0; document.getElementById(key).innerText = 0; });
        customItems = [];
        document.getElementById('customItemsContainer').innerHTML = '';
        document.querySelector('input[name="base"][value="400"]').checked = true;
        calculateTotal();
    }

    // 綁定基本款式的點擊事件
    document.querySelectorAll('input[name="base"]').forEach(radio => {
        radio.addEventListener('change', calculateTotal);
    });
</script>

</body>
</html>
