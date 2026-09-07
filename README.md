<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>这一天在FDU吃了什么</title>
    <style>
        :root {
            --primary: #1E88E5;
            --primary-light: #64B5F6;
            --primary-dark: #1565C0;
            --bg: #F5F9FF;
            --card-bg: #FFFFFF;
            --text: #1E2A3A;
            --text-secondary: #6B7A8C;
            --border: #DDE6F0;
            --note-color: #FF3B30;
            --note-bg: #FFF0EE;
            --note-border: #FFD4D1;
            --shadow: 0 4px 20px rgba(30, 136, 229, 0.1);
            --radius: 16px;
            --radius-sm: 10px;
            --transition: 0.25s cubic-bezier(0.4, 0, 0.2, 1);
        }
        * { margin: 0; padding: 0; box-sizing: border-box; -webkit-tap-highlight-color: transparent; }
        body {
            font-family: -apple-system, 'PingFang SC', 'Hiragino Sans GB', 'Microsoft YaHei', 'Noto Sans SC', sans-serif;
            background: var(--bg); color: var(--text); min-height: 100vh; padding-bottom: 100px;
            overflow-x: hidden; -webkit-font-smoothing: antialiased;
        }
        .top-bar { position: sticky; top: 0; z-index: 100; background: rgba(245,249,255,0.92); backdrop-filter: blur(20px); -webkit-backdrop-filter: blur(20px); border-bottom: 1px solid var(--border); padding: 14px 20px; display: flex; align-items: center; justify-content: space-between; gap: 12px; }
        .top-bar .logo { font-size: 16px; font-weight: 800; color: var(--primary); display: flex; align-items: center; gap: 6px; cursor: pointer; user-select: none; white-space: nowrap; overflow: hidden; }
        .top-bar .logo .icon { font-size: 24px; flex-shrink: 0; }
        .top-bar .logo .title-text { white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
        .top-bar .actions { display: flex; gap: 8px; align-items: center; flex-shrink: 0; }
        .icon-btn { width: 40px; height: 40px; border-radius: 50%; border: none; background: var(--card-bg); cursor: pointer; font-size: 18px; display: flex; align-items: center; justify-content: center; box-shadow: var(--shadow); transition: var(--transition); color: var(--text); user-select: none; }
        .icon-btn:active { transform: scale(0.9); }
        .calendar-container { max-width: 520px; margin: 0 auto; padding: 12px 12px 6px; }
        .calendar-header { display: flex; align-items: center; justify-content: space-between; margin-bottom: 10px; padding: 0 4px; }
        .calendar-header .month-label { font-size: 19px; font-weight: 700; color: var(--primary-dark); }
        .calendar-header .nav-btns { display: flex; gap: 6px; }
        .calendar-header .nav-btn { width: 36px; height: 36px; border-radius: 50%; border: none; background: var(--card-bg); cursor: pointer; font-size: 16px; display: flex; align-items: center; justify-content: center; box-shadow: var(--shadow); transition: var(--transition); color: var(--text); }
        .calendar-weekdays { display: grid; grid-template-columns: repeat(7, 1fr); text-align: center; font-size: 12px; font-weight: 600; color: var(--text-secondary); margin-bottom: 4px; }
        .calendar-weekdays span { padding: 4px 0; }
        .calendar-days { display: grid; grid-template-columns: repeat(7, 1fr); gap: 4px; }
        .calendar-day { aspect-ratio: 1; border-radius: 12px; border: none; background: transparent; cursor: pointer; font-size: 14px; font-weight: 500; display: flex; flex-direction: column; align-items: center; justify-content: center; transition: all 0.2s; position: relative; color: var(--text); user-select: none; gap: 2px; padding: 2px; overflow: hidden; }
        .calendar-day:hover { background: #E3F2FD; }
        .calendar-day.other-month { color: #B0C4DE; opacity: 0.55; }
        .calendar-day.today { background: var(--primary); color: #fff; font-weight: 700; box-shadow: 0 4px 14px rgba(30,136,229,0.35); }
        .calendar-day.today:hover { background: var(--primary-dark); }
        .calendar-day.selected { outline: 2.5px solid var(--primary); outline-offset: 1px; background: #E3F2FD; }
        .calendar-day.today.selected { outline-color: var(--primary-dark); }
        .calendar-day .day-num { font-size: 13px; font-weight: 600; z-index: 2; }
        .calendar-day .day-photo { position: absolute; top: 0; left: 0; width: 100%; height: 100%; object-fit: cover; border-radius: 10px; opacity: 0.35; z-index: 1; }
        .calendar-day .dot { width: 5px; height: 5px; border-radius: 50%; background: var(--primary); flex-shrink: 0; z-index: 2; }
        .calendar-day.today .dot { background: #fff; }
        .calendar-day .count-badge { position: absolute; top: 2px; right: 4px; font-size: 8px; font-weight: 700; color: #fff; background: var(--primary); border-radius: 6px; padding: 0 4px; min-width: 14px; text-align: center; z-index: 3; }
        .calendar-day.today .count-badge { background: rgba(0,0,0,0.3); }

        .day-records { max-width: 520px; margin: 0 auto; padding: 8px 16px 20px; }
        .day-records .section-title { font-size: 15px; font-weight: 700; margin-bottom: 10px; color: var(--primary-dark); }
        .record-card { background: var(--card-bg); border-radius: var(--radius); padding: 14px; margin-bottom: 12px; box-shadow: var(--shadow); position: relative; border: 1px solid #EBF0F8; }
        .record-card .food-name { font-size: 17px; font-weight: 800; margin-bottom: 4px; }
        .record-card .photo { width: 100%; max-height: 220px; object-fit: cover; border-radius: var(--radius-sm); margin-bottom: 8px; background: #F5F9FF; }
        .record-card .tags-row { display: flex; flex-wrap: wrap; gap: 5px; margin-bottom: 6px; }
        .tag { display: inline-flex; align-items: center; gap: 3px; padding: 3px 10px; border-radius: 16px; font-size: 11px; font-weight: 600; background: #E3F2FD; color: var(--primary-dark); }
        .tag.tag-canteen { background: #E8F5E9; color: #2E7D32; }
        .tag.tag-meal { background: #E3F2FD; color: #1565C0; }
        .tag.tag-portion { background: #FFF3E0; color: #E65100; }
        .record-card .review-text { font-size: 14px; line-height: 1.5; margin-bottom: 4px; }
        .record-card .note-box { background: var(--note-bg); border-left: 4px solid var(--note-color); padding: 8px 12px; border-radius: 0 var(--radius-sm) var(--radius-sm) 0; font-size: 12px; color: #B71C1C; margin-top: 6px; display: flex; gap: 6px; font-weight: 500; }
        .record-card .card-actions { position: absolute; top: 8px; right: 8px; display: flex; gap: 6px; opacity: 0; transition: var(--transition); }
        .record-card:hover .card-actions { opacity: 1; }
        .record-card .action-btn { width: 30px; height: 30px; border-radius: 50%; border: none; background: rgba(255,255,255,0.9); cursor: pointer; font-size: 14px; display: flex; align-items: center; justify-content: center; box-shadow: 0 2px 8px rgba(0,0,0,0.1); color: #E53935; }
        .record-card .action-btn.edit-btn { color: var(--primary); }
        .empty-state { text-align: center; padding: 30px 20px; color: var(--text-secondary); }
        .empty-state .emoji { font-size: 48px; margin-bottom: 12px; }
        .fab { position: fixed; bottom: 24px; left: 50%; transform: translateX(-50%); width: 56px; height: 56px; border-radius: 50%; border: none; background: var(--primary); color: #fff; font-size: 28px; cursor: pointer; box-shadow: 0 6px 24px rgba(30,136,229,0.45); transition: all 0.3s; display: flex; align-items: center; justify-content: center; z-index: 200; }
        .fab:active { transform: translateX(-50%) scale(0.88); }

        .wordcloud-panel { max-width: 520px; margin: 0 auto; padding: 16px; }
        .wordcloud-title { font-size: 18px; font-weight: 800; color: var(--primary-dark); margin-bottom: 12px; text-align: center; }
        .wordcloud-container { background: var(--card-bg); border-radius: var(--radius); padding: 20px; box-shadow: var(--shadow); min-height: 260px; display: flex; flex-wrap: wrap; align-items: center; justify-content: center; gap: 12px; }
        .wordcloud-word { display: inline-block; padding: 6px 14px; border-radius: 20px; font-weight: 700; transition: transform 0.2s; cursor: default; white-space: nowrap; }
        .wordcloud-word:hover { transform: scale(1.1); }
        .wordcloud-word.rank-1 { font-size: 28px; background: #FFEBEE; color: #C62828; }
        .wordcloud-word.rank-2 { font-size: 24px; background: #FFF3E0; color: #E65100; }
        .wordcloud-word.rank-3 { font-size: 20px; background: #FFF8E1; color: #F57F17; }
        .wordcloud-word.rank-4 { font-size: 16px; background: #E3F2FD; color: #1565C0; }
        .wordcloud-word.rank-5 { font-size: 14px; background: #F3E5F5; color: #6A1B9A; }
        .wordcloud-word.rank-6 { font-size: 12px; background: #E8F5E9; color: #2E7D32; }

        .modal-overlay { position: fixed; inset: 0; background: rgba(0,0,0,0.45); z-index: 300; display: none; align-items: flex-end; justify-content: center; backdrop-filter: blur(4px); }
        .modal-overlay.active { display: flex; }
        .modal-sheet { background: var(--card-bg); border-radius: 24px 24px 0 0; width: 100%; max-width: 560px; max-height: 88vh; overflow-y: auto; padding: 20px 20px 30px; }
        .modal-handle { width: 40px; height: 4px; border-radius: 4px; background: #D0DCEB; margin: 0 auto 16px; }
        .modal-title { font-size: 20px; font-weight: 800; margin-bottom: 16px; text-align: center; color: var(--primary-dark); }
        .form-group { margin-bottom: 14px; }
        .form-group label { display: block; font-size: 13px; font-weight: 700; color: var(--text-secondary); margin-bottom: 4px; }
        .form-input { width: 100%; padding: 10px 14px; border-radius: var(--radius-sm); border: 1.5px solid var(--border); font-size: 14px; outline: none; background: #FFFDFB; font-family: inherit; }
        .form-input:focus { border-color: var(--primary); box-shadow: 0 0 0 3px rgba(30,136,229,0.12); }
        .tag-selector { display: flex; flex-wrap: wrap; gap: 6px; }
        .tag-option { padding: 6px 12px; border-radius: 18px; border: 1.5px solid var(--border); background: #FFFDFB; cursor: pointer; font-size: 12px; font-weight: 600; color: var(--text-secondary); }
        .tag-option.selected { background: var(--primary); color: #fff; border-color: var(--primary); }
        .tag-option.tag-canteen.selected { background: #2E7D32; border-color: #2E7D32; }
        .tag-option.tag-meal.selected { background: #1565C0; border-color: #1565C0; }
        .tag-option.tag-portion.selected { background: #E65100; border-color: #E65100; }
        .custom-input-row { display: flex; gap: 6px; margin-top: 6px; }
        .custom-input-row .form-input { flex: 1; }
        .custom-input-row .add-btn { padding: 8px 14px; border-radius: 16px; border: none; background: var(--primary-light); color: #fff; font-weight: 700; font-size: 12px; cursor: pointer; }
        .note-input-wrap { position: relative; }
        .note-input-wrap .form-input { border-color: var(--note-border); background: var(--note-bg); color: #8B1A1A; padding-right: 35px; }
        .note-input-wrap .note-emoji { position: absolute; right: 12px; top: 50%; transform: translateY(-50%); }
        .photo-upload { border: 2px dashed var(--border); border-radius: var(--radius-sm); padding: 16px; text-align: center; cursor: pointer; background: #FFFDFB; }
        .photo-upload img.preview { max-width: 100%; max-height: 180px; border-radius: 8px; margin-top: 8px; }
        .photo-upload .remove-photo { position: absolute; top: 8px; right: 8px; width: 28px; height: 28px; border-radius: 50%; border: none; background: rgba(0,0,0,0.5); color: #fff; cursor: pointer; }
        .submit-btn { width: 100%; padding: 14px; border-radius: var(--radius-sm); border: none; background: var(--primary); color: #fff; font-size: 16px; font-weight: 700; cursor: pointer; margin-top: 8px; }
        .search-panel { max-width: 520px; margin: 0 auto; padding: 16px; }
        .search-panel .search-input { width: 100%; padding: 12px 16px; border-radius: 22px; border: 2px solid var(--border); font-size: 14px; outline: none; }
        .filter-tags { display: flex; flex-wrap: wrap; gap: 6px; margin-top: 8px; }
        .filter-tag { padding: 6px 12px; border-radius: 16px; border: 1.5px solid var(--border); background: var(--card-bg); cursor: pointer; font-size: 12px; font-weight: 600; color: var(--text-secondary); }
        .filter-tag.active { background: var(--primary); color: #fff; border-color: var(--primary); }
        .toast { position: fixed; bottom: 90px; left: 50%; transform: translateX(-50%); background: #1E2A3A; color: #fff; padding: 10px 20px; border-radius: 20px; font-size: 13px; font-weight: 600; opacity: 0; pointer-events: none; transition: all 0.3s; z-index: 500; }
        .toast.show { opacity: 1; }
    </style>
</head>
<body>
    <header class="top-bar">
        <div class="logo" id="editableTitle" title="点击修改标题">
            <span class="icon">🍜</span>
            <span class="title-text" id="titleText">这一天在FDU吃了什么</span>
        </div>
        <div class="actions">
            <button class="icon-btn" id="btnWordCloud" title="词云统计">☁️</button>
            <button class="icon-btn" id="btnSearch" title="搜索">🔍</button>
        </div>
    </header>

    <div class="calendar-container" id="calendarSection">
        <div class="calendar-header">
            <button class="nav-btn" id="btnPrevMonth">◀</button>
            <span class="month-label" id="monthLabel"></span>
            <button class="nav-btn" id="btnNextMonth">▶</button>
        </div>
        <div class="calendar-weekdays"><span>日</span><span>一</span><span>二</span><span>三</span><span>四</span><span>五</span><span>六</span></div>
        <div class="calendar-days" id="calendarDays"></div>
    </div>

    <div class="day-records" id="dayRecordsSection">
        <div class="section-title" id="recordsTitle"></div>
        <div id="recordsList"></div>
    </div>

    <div class="wordcloud-panel" id="wordcloudPanel" style="display:none;">
        <div class="wordcloud-title">☁️ 我的食物词云</div>
        <div class="wordcloud-container" id="wordcloudContainer"></div>
        <div style="text-align:center;margin-top:16px;"><button class="icon-btn" id="btnBackFromWordCloud" style="width:auto;padding:10px 24px;border-radius:22px;font-size:14px;font-weight:600;">← 返回日历</button></div>
    </div>

    <div class="search-panel" id="searchPanel" style="display:none;">
        <input type="text" class="search-input" id="searchKeyword" placeholder="🔍 搜索食物名称、评价..." autocomplete="off">
        <div class="filter-tags" id="filterCanteens"></div>
        <div class="filter-tags" id="filterMealTypes"></div>
        <div class="filter-tags" id="filterPortions"></div>
        <div class="filter-tags" id="filterHasNote"><button class="filter-tag filter-note" data-value="has_note">⚠️ 有注意</button></div>
        <div class="search-results-count" id="searchCount"></div>
        <div id="searchResults"></div>
        <div style="text-align:center;margin-top:12px;"><button class="icon-btn" id="btnBackToCalendar" style="width:auto;padding:10px 24px;border-radius:22px;font-size:14px;font-weight:600;">← 返回日历</button></div>
    </div>

    <button class="fab" id="fabAdd">+</button>

    <div class="modal-overlay" id="modalOverlay">
        <div class="modal-sheet">
            <div class="modal-handle"></div>
            <div class="modal-title" id="modalTitle">🍽️ 记录今天的美味</div>
            <div class="form-group"><label>🍛 食物名称</label><input type="text" class="form-input" id="foodNameInput" placeholder="多个食物用空格或、分隔"></div>
            <div class="form-group"><label>📸 照片</label><div class="photo-upload" id="photoUpload"><span id="uploadIcon">📷 点击上传</span><img class="preview" id="photoPreview" style="display:none;"><button class="remove-photo" id="btnRemovePhoto" style="display:none;">✕</button><input type="file" id="fileInput" accept="image/*" style="display:none;"></div></div>
            <div class="form-group"><label>🏫 食堂名称</label><div class="tag-selector" id="canteenSelector"></div><div class="custom-input-row" id="customCanteenRow" style="display:none;"><input type="text" class="form-input" id="customCanteenInput" placeholder="新食堂名称"><button class="add-btn" id="btnAddCustomCanteen">添加</button></div></div>
            <div class="form-group"><label>🍽️ 用餐类型</label><div class="tag-selector" id="mealTypeSelector"></div><div class="custom-input-row" id="customMealRow" style="display:none;"><input type="text" class="form-input" id="customMealInput" placeholder="新类型"><button class="add-btn" id="btnAddCustomMeal">添加</button></div></div>
            <div class="form-group"><label>⚖️ 分量</label><div class="tag-selector" id="portionSelector"></div></div>
            <div class="form-group"><label>💬 我的评价</label><textarea class="form-input" id="reviewInput" rows="2"></textarea></div>
            <div class="form-group"><label>⚠️ 注意</label><div class="note-input-wrap"><input type="text" class="form-input" id="noteInput" placeholder="排队超长！微辣！"><span>⚠️</span></div></div>
            <button class="submit-btn" id="btnSubmit">保存记录 ✓</button>
        </div>
    </div>

    <div class="toast" id="toast"></div>

    <script>
        (function() {
            const STORAGE_KEY = 'fdu_eat_diary_v1';
            const CUSTOM_CANTEENS_KEY = 'fdu_eat_diary_canteens_v1';
            const CUSTOM_MEALS_KEY = 'fdu_eat_diary_meals_v1';
            const TITLE_KEY = 'fdu_eat_diary_title_v1';
            const DEFAULT_TITLE = '这一天在FDU吃了什么';
            const DEFAULT_CANTEENS = ['北食', '南食', '旦苑', '其他'];
            const DEFAULT_MEAL_TYPES = ['早饭', '正餐', '饮料', '甜点'];
            const DEFAULT_PORTIONS = ['量少', '正好', '量多'];
            let allData = {};
            let customCanteens = [];
            let customMealTypes = [];
            let currentYear = new Date().getFullYear();
            let currentMonth = new Date().getMonth();
            let selectedDate = formatDate(new Date());
            let selectedCanteen = null;
            let selectedMealType = null;
            let selectedPortion = null;
            let photoDataUrl = null;
            let editingRecordId = null;
            let editingDate = null;
            let activeSearchFilters = { canteen: null, mealType: null, portion: null, hasNote: false, keyword: '' };

            function formatDate(date) { const y = date.getFullYear(); const m = String(date.getMonth() + 1).padStart(2, '0'); const d = String(date.getDate()).padStart(2, '0'); return `${y}-${m}-${d}`; }
            function getTodayStr() { return formatDate(new Date()); }
            function generateId() { return Date.now().toString(36) + Math.random().toString(36).substr(2, 6); }

            function loadTitle() { try { return localStorage.getItem(TITLE_KEY) || DEFAULT_TITLE; } catch(e) { return DEFAULT_TITLE; } }
            function saveTitle(title) { try { localStorage.setItem(TITLE_KEY, title); } catch(e) {} }

            function loadData() {
                try { allData = JSON.parse(localStorage.getItem(STORAGE_KEY)) || {}; } catch(e) { allData = {}; }
                try { customCanteens = JSON.parse(localStorage.getItem(CUSTOM_CANTEENS_KEY)) || []; } catch(e) { customCanteens = []; }
                try { customMealTypes = JSON.parse(localStorage.getItem(CUSTOM_MEALS_KEY)) || []; } catch(e) { customMealTypes = []; }
            }
            function saveData() {
                try { localStorage.setItem(STORAGE_KEY, JSON.stringify(allData)); } catch(e) {}
                try { localStorage.setItem(CUSTOM_CANTEENS_KEY, JSON.stringify(customCanteens)); } catch(e) {}
                try { localStorage.setItem(CUSTOM_MEALS_KEY, JSON.stringify(customMealTypes)); } catch(e) {}
            }

            function getAllCanteens() { return [...new Set([...DEFAULT_CANTEENS, ...customCanteens])]; }
            function getAllMealTypes() { return [...new Set([...DEFAULT_MEAL_TYPES, ...customMealTypes])]; }
            function getRecordsForDate(dateStr) { return allData[dateStr] || []; }

            function splitFoodName(name) {
                if (!name) return [];
                // 按空格、逗号、顿号、分号、竖线等分隔
                return name.split(/[\s,，、;；|/]+/).map(s => s.trim()).filter(s => s.length > 0);
            }

            function showToast(msg) { const t = document.getElementById('toast'); t.textContent = msg; t.classList.add('show'); clearTimeout(t._timeout); t._timeout = setTimeout(() => t.classList.remove('show'), 1800); }

            function compressImage(file, callback) {
                const reader = new FileReader();
                reader.onload = function(e) { const img = new Image(); img.onload = function() { const canvas = document.createElement('canvas'); let w = img.width, h = img.height; const max = 600; if (w > max || h > max) { const ratio = Math.min(max/w, max/h); w = Math.round(w*ratio); h = Math.round(h*ratio); } canvas.width = w; canvas.height = h; canvas.getContext('2d').drawImage(img, 0, 0, w, h); callback(canvas.toDataURL('image/jpeg', 0.6)); }; img.src = e.target.result; };
                reader.readAsDataURL(file);
            }

            function renderCalendar() {
                document.getElementById('monthLabel').textContent = `${currentYear}年${currentMonth + 1}月`;
                const container = document.getElementById('calendarDays');
                container.innerHTML = '';
                const firstDay = new Date(currentYear, currentMonth, 1).getDay();
                const daysInMonth = new Date(currentYear, currentMonth + 1, 0).getDate();
                const daysInPrevMonth = new Date(currentYear, currentMonth, 0).getDate();
                const todayStr = getTodayStr();
                const totalCells = Math.ceil((firstDay + daysInMonth) / 7) * 7;
                for (let i = 0; i < totalCells; i++) {
                    const dayNum = i - firstDay + 1;
                    let displayDay, dateObj, isOtherMonth = false;
                    if (dayNum <= 0) { displayDay = daysInPrevMonth + dayNum; dateObj = new Date(currentYear, currentMonth - 1, displayDay); isOtherMonth = true; }
                    else if (dayNum > daysInMonth) { displayDay = dayNum - daysInMonth; dateObj = new Date(currentYear, currentMonth + 1, displayDay); isOtherMonth = true; }
                    else { displayDay = dayNum; dateObj = new Date(currentYear, currentMonth, displayDay); }
                    const dateStr = formatDate(dateObj);
                    const records = getRecordsForDate(dateStr);
                    const firstPhoto = records.find(r => r.photo)?.photo;
                    const isToday = dateStr === todayStr;
                    const isSelected = dateStr === selectedDate;
                    const btn = document.createElement('button');
                    btn.className = 'calendar-day'; if (isOtherMonth) btn.classList.add('other-month'); if (isToday) btn.classList.add('today'); if (isSelected) btn.classList.add('selected');
                    btn.innerHTML = `<span class="day-num">${displayDay}</span>${firstPhoto ? `<img class="day-photo" src="${firstPhoto}">` : ''}${records.length > 0 ? '<span class="dot"></span>' : ''}${records.length > 1 ? `<span class="count-badge">${records.length}</span>` : ''}`;
                    btn.addEventListener('click', () => { selectedDate = dateStr; if (isOtherMonth) { if (dayNum <= 0) { currentMonth--; if (currentMonth < 0) { currentMonth = 11; currentYear--; } } else { currentMonth++; if (currentMonth > 11) { currentMonth = 0; currentYear++; } } } renderCalendar(); renderDayRecords(); document.getElementById('wordcloudPanel').style.display = 'none'; document.getElementById('calendarSection').style.display = 'block'; document.getElementById('dayRecordsSection').style.display = 'block'; document.getElementById('searchPanel').style.display = 'none'; });
                    container.appendChild(btn);
                }
            }

            function renderDayRecords() {
                const titleEl = document.getElementById('recordsTitle');
                const listEl = document.getElementById('recordsList');
                const dateObj = new Date(selectedDate + 'T00:00:00');
                titleEl.textContent = `📅 ${dateObj.getFullYear()}年${dateObj.getMonth()+1}月${dateObj.getDate()}日`;
                const records = getRecordsForDate(selectedDate);
                if (!records.length) { listEl.innerHTML = '<div class="empty-state"><div class="emoji">🍽️</div>还没有记录</div>'; return; }
                listEl.innerHTML = records.map(rec => `
                    <div class="record-card">
                        <div class="card-actions"><button class="action-btn edit-btn" data-id="${rec.id}">✏️</button><button class="action-btn" data-id="${rec.id}">🗑️</button></div>
                        <div class="food-name">${rec.name}</div>
                        ${rec.photo ? `<img class="photo" src="${rec.photo}">` : ''}
                        <div class="tags-row"><span class="tag tag-canteen">🏫${rec.canteen}</span><span class="tag tag-meal">🍽️${rec.mealType}</span>${rec.portion ? `<span class="tag tag-portion">⚖️${rec.portion}</span>` : ''}</div>
                        ${rec.review ? `<div class="review-text">${rec.review}</div>` : ''}
                        ${rec.note ? `<div class="note-box">⚠️ ${rec.note}</div>` : ''}
                    </div>
                `).join('');
                listEl.querySelectorAll('.edit-btn').forEach(b => b.onclick = () => openEditModal(selectedDate, b.dataset.id));
                listEl.querySelectorAll('.action-btn:not(.edit-btn)').forEach(b => b.onclick = () => deleteRecord(selectedDate, b.dataset.id));
            }

            function deleteRecord(dateStr, id) { if (!confirm('删除这条记录？')) return; allData[dateStr] = (allData[dateStr]||[]).filter(r => r.id !== id); if (!allData[dateStr].length) delete allData[dateStr]; saveData(); renderCalendar(); renderDayRecords(); }

            function renderWordCloud() {
                const container = document.getElementById('wordcloudContainer');
                const allFoods = [];
                Object.values(allData).forEach(records => records.forEach(r => { splitFoodName(r.name).forEach(f => allFoods.push(f)); }));
                if (!allFoods.length) { container.innerHTML = '<div class="empty-state">还没有食物记录</div>'; return; }
                const counts = {};
                allFoods.forEach(f => counts[f] = (counts[f] || 0) + 1);
                const sorted = Object.entries(counts).sort((a,b) => b[1] - a[1]);
                container.innerHTML = sorted.map(([word, count], i) => {
                    const rank = Math.min(i + 1, 6);
                    return `<span class="wordcloud-word rank-${rank}" title="出现${count}次">${word} ×${count}</span>`;
                }).join('');
            }

            function resetForm() {
                photoDataUrl = null; selectedCanteen = null; selectedMealType = null; selectedPortion = null;
                document.getElementById('foodNameInput').value = ''; document.getElementById('reviewInput').value = ''; document.getElementById('noteInput').value = '';
                document.getElementById('photoPreview').style.display = 'none'; document.getElementById('uploadIcon').style.display = 'block'; document.getElementById('btnRemovePhoto').style.display = 'none';
                editingRecordId = null; editingDate = null; renderTagSelectors();
            }

            function renderTagSelectors() {
                document.getElementById('canteenSelector').innerHTML = getAllCanteens().map(c => `<span class="tag-option tag-canteen ${selectedCanteen===c?'selected':''}" data-canteen="${c}">${c}</span>`).join('') + '<span class="tag-option" id="customCanteenBtn">+</span>';
                document.getElementById('mealTypeSelector').innerHTML = getAllMealTypes().map(m => `<span class="tag-option tag-meal ${selectedMealType===m?'selected':''}" data-meal="${m}">${m}</span>`).join('') + '<span class="tag-option" id="customMealBtn">+</span>';
                document.getElementById('portionSelector').innerHTML = DEFAULT_PORTIONS.map(p => `<
