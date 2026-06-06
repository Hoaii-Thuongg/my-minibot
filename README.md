<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>SUPERGARDENING</title>
    <script src="https://telegram.org/js/telegram-web-app.js"></script>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, sans-serif;
            background: linear-gradient(135deg, #e8f5e9 0%, #fff8e1 100%);
            color: #2e3b2c;
            min-height: 100vh;
            padding-bottom: 70px;
            transition: background 0.3s, color 0.3s;
        }
        .container { max-width: 480px; margin: 0 auto; padding: 12px; }
        .header {
            background: linear-gradient(90deg, #43a047, #66bb6a);
            color: white;
            border-radius: 16px;
            padding: 15px 20px;
            margin-bottom: 12px;
            box-shadow: 0 4px 12px rgba(76,175,80,0.3);
            text-align: center;
        }
        .header h1 { font-size: 24px; display: flex; align-items: center; justify-content: center; gap: 8px; }
        .card {
            background: white;
            border-radius: 20px;
            padding: 16px;
            margin-bottom: 12px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.05);
        }
        .card-title { font-weight: bold; font-size: 18px; margin-bottom: 12px; display: flex; align-items: center; gap: 8px; }
        .grid-2 { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
        .grid-3 { display: grid; grid-template-columns: repeat(3,1fr); gap: 10px; }
        .fruit-card {
            background: #f1f8e9;
            border-radius: 16px;
            padding: 12px 8px;
            text-align: center;
            cursor: pointer;
            transition: transform 0.2s;
            border: 2px solid transparent;
        }
        .fruit-card:active { transform: scale(0.95); }
        .fruit-card.selected { border-color: #ffb74d; background: #fff3e0; }
        .fruit-emoji { font-size: 40px; display: block; }
        .btn {
            background: linear-gradient(90deg, #43a047, #66bb6a);
            color: white;
            border: none;
            border-radius: 25px;
            padding: 12px 20px;
            font-weight: bold;
            font-size: 16px;
            cursor: pointer;
            width: 100%;
            transition: opacity 0.2s;
            box-shadow: 0 4px 10px rgba(76,175,80,0.3);
        }
        .btn:active { opacity: 0.8; }
        .btn-small {
            padding: 8px 16px;
            font-size: 14px;
            width: auto;
            display: inline-block;
            margin: 4px;
        }
        .btn-danger { background: linear-gradient(90deg, #ef5350, #e57373); }
        .btn-outline {
            background: white;
            border: 2px solid #43a047;
            color: #43a047;
            box-shadow: none;
        }
        .balance { font-size: 28px; font-weight: bold; color: #2e7d32; margin: 8px 0; }
        .tab-nav {
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            background: white;
            display: flex;
            justify-content: space-around;
            padding: 8px 0;
            box-shadow: 0 -2px 10px rgba(0,0,0,0.1);
            z-index: 100;
            border-top-left-radius: 20px;
            border-top-right-radius: 20px;
        }
        .tab-item {
            flex: 1;
            text-align: center;
            padding: 5px;
            color: #757575;
            font-size: 14px;
            cursor: pointer;
            transition: all 0.2s;
            border-radius: 12px;
            margin: 0 4px;
        }
        .tab-item.active { color: #2e7d32; font-weight: bold; background: #e8f5e9; }
        .page { display: none; }
        .page.active { display: block; }
        .notification { background: #fff9c4; border-left: 4px solid #ffb300; padding: 10px; border-radius: 8px; margin-bottom: 8px; }
        .event { background: #e1f5fe; border-radius: 12px; padding: 12px; margin-bottom: 8px; }
        .rank-item {
            display: flex;
            align-items: center;
            gap: 10px;
            padding: 10px;
            border-bottom: 1px solid #eee;
        }
        .rank-number { font-weight: bold; font-size: 20px; width: 30px; }
        .team-card { background: #f0f4c3; border-radius: 14px; padding: 12px; margin-bottom: 8px; }
        input, select {
            width: 100%;
            padding: 12px;
            border-radius: 12px;
            border: 1px solid #c8e6c9;
            background: #f9fbe7;
            margin: 8px 0;
            font-size: 16px;
        }
        .hidden { display: none; }
        .modal {
            position: fixed;
            top: 0; left: 0; right: 0; bottom: 0;
            background: rgba(0,0,0,0.5);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 200;
        }
        .modal-content {
            background: white;
            border-radius: 20px;
            padding: 20px;
            width: 90%;
            max-width: 400px;
        }
    </style>
</head>
<body>
<div class="container">
    <!-- HEADER -->
    <div class="header">
        <h1>🌱 SUPERGARDENING</h1>
        <p style="font-size:14px; opacity:0.9;">Trồng cây – Thu quả ngọt</p>
    </div>

    <!-- PAGES -->
    <!-- TRANG CHỦ -->
    <div id="page-home" class="page active">
        <div class="card">
            <div class="card-title">📢 Thông báo</div>
            <div class="notification">🎉 Chào mừng nhà đầu tư mới! Nhận ngay 5.000đ khi đăng ký.</div>
            <div class="notification">⭐ Sự kiện mùa hè: Lãi suất x2 cho gói Dưa hấu và Đào trong tuần này!</div>
        </div>
        <div class="card">
            <div class="card-title">📅 Điểm danh hằng ngày</div>
            <p>Nhận <b>1.000đ</b> mỗi ngày</p>
            <button class="btn" id="checkin-btn" style="margin-top:8px;">✅ Điểm danh (+1.000đ)</button>
            <p style="margin-top:4px; font-size:12px; color:#888;" id="checkin-status"></p>
        </div>
        <div class="card">
            <div class="card-title">📞 Hỗ trợ Admin</div>
            <p>Telegram: <a href="https://t.me/admin_supergardening" target="_blank">@admin_supergardening</a></p>
            <p>Email: support@supergardening.vn</p>
        </div>
    </div>

    <!-- BẢNG XẾP HẠNG -->
    <div id="page-leaderboard" class="page">
        <div class="card">
            <div class="card-title">🏆 Top 10 Người Trồng Cây</div>
            <div id="leaderboard-list"></div>
        </div>
    </div>

    <!-- ĐỘI NHÓM -->
    <div id="page-team" class="page">
        <div class="card">
            <div class="card-title">👥 Đội của tôi</div>
            <p>Bạn nhận <b>15%</b> từ lãi của người bạn mời trực tiếp (F1)</p>
            <button class="btn btn-outline" id="copy-ref-link">🔗 Sao chép link giới thiệu</button>
            <div id="team-list" style="margin-top:12px;"></div>
        </div>
    </div>

    <!-- TÀI KHOẢN -->
    <div id="page-account" class="page">
        <div class="card">
            <div class="card-title">👤 Tài khoản</div>
            <p>Tên: <span id="user-name">...</span></p>
            <p>ID: <span id="user-id">...</span></p>
            <p class="balance" id="balance-display">0đ</p>
            <button class="btn" id="deposit-btn" style="margin-top:8px;">💰 Nạp tiền (Demo)</button>
        </div>
        <div class="card">
            <div class="card-title">🌿 Đầu tư</div>
            <p>Chọn gói:</p>
            <div class="grid-3" id="package-list"></div>
            <button class="btn" id="invest-btn" style="margin-top:8px;">🌱 Đầu tư</button>
            <div id="investment-status" style="margin-top:8px; font-size:14px;"></div>
        </div>
        <div class="card">
            <div class="card-title">💸 Rút tiền</div>
            <p>Min: 20k – Phí: 2% (20k-<50k), 5% (50k-<100k), 7% (>=100k)</p>
            <input type="number" id="withdraw-amount" placeholder="Nhập số tiền rút" min="20000">
            <button class="btn btn-danger" id="withdraw-btn">Rút ngay</button>
            <p style="font-size:12px; color:#888;" id="withdraw-status"></p>
        </div>
    </div>
</div>

<!-- TAB NAV -->
<div class="tab-nav">
    <div class="tab-item active" data-page="home">🏠 Trang chủ</div>
    <div class="tab-item" data-page="leaderboard">🏆 Xếp hạng</div>
    <div class="tab-item" data-page="team">👥 Đội nhóm</div>
    <div class="tab-item" data-page="account">👤 Tài khoản</div>
</div>

<!-- MODAL NẠP TIỀN -->
<div id="deposit-modal" class="modal hidden">
    <div class="modal-content">
        <h3>Nạp tiền thử nghiệm</h3>
        <input type="number" id="deposit-amount-input" placeholder="Số tiền (VNĐ)" min="10000">
        <p style="font-size:12px;">Nạp từ 6h-18h: lãi tính từ hôm sau. Sau 18h: tính từ hôm kia.</p>
        <button class="btn" id="confirm-deposit">Xác nhận</button>
        <button class="btn btn-outline" id="close-deposit">Đóng</button>
    </div>
</div>

<script>
    // ========== CẤU HÌNH ==========
    const PACKAGES = [
        { name: 'Dâu', emoji: '🍓', amount: 50000, rate: 0.02 },
        { name: 'Cam', emoji: '🍊', amount: 100000, rate: 0.025 },
        { name: 'Nho', emoji: '🍇', amount: 400000, rate: 0.03 },
        { name: 'Dưa hấu', emoji: '🍉', amount: 800000, rate: 0.035 },
        { name: 'Đào', emoji: '🍑', amount: 1000000, rate: 0.04 },
        { name: 'Cherry', emoji: '🍒', amount: 1200000, rate: 0.045 },
        { name: 'Kiwi', emoji: '🥝', amount: 1500000, rate: 0.05 }
    ];

    // ========== TELEGRAM ==========
    const tg = window.Telegram.WebApp;
    tg.ready();
    const user = tg.initDataUnsafe?.user || { first_name: 'Người dùng', id: 'local' };
    const userId = user.id.toString();
    document.getElementById('user-name').textContent = user.first_name || 'Bạn';
    document.getElementById('user-id').textContent = userId;

    // ========== LƯU TRỮ ==========
    function getData(key) {
        try {
            return JSON.parse(localStorage.getItem(`sg_${userId}_${key}`));
        } catch(e) { return null; }
    }
    function setData(key, value) {
        localStorage.setItem(`sg_${userId}_${key}`, JSON.stringify(value));
    }
    function getBalance() { return getData('balance') || 0; }
    function setBalance(val) { setData('balance', val); }
    function getInvestments() { return getData('investments') || []; }
    function setInvestments(arr) { setData('investments', arr); }

    // ========== TIỆN ÍCH ==========
    function formatCurrency(num) {
        return num.toLocaleString('vi-VN') + 'đ';
    }
    function todayStr() {
        return new Date().toISOString().slice(0,10);
    }
    function addDays(dateStr, days) {
        let d = new Date(dateStr);
        d.setDate(d.getDate() + days);
        return d.toISOString().slice(0,10);
    }
    function daysBetween(date1, date2) {
        // date1 < date2, returns number of days
        return Math.floor((new Date(date2) - new Date(date1)) / 86400000);
    }

    // ========== CẬP NHẬT LÃI ==========
    function updateAllProfits() {
        let investments = getInvestments();
        let balance = getBalance();
        let changed = false;
        const today = todayStr();
        investments.forEach(inv => {
            if (!inv.lastProfitDate) inv.lastProfitDate = inv.startDate;
            if (today > inv.lastProfitDate) {
                // calculate profit for each day from lastProfitDate+1 to today
                let start = inv.lastProfitDate;
                let end = today;
                let days = daysBetween(start, end);
                if (days > 0) {
                    let profit = Math.floor(inv.amount * inv.rate * days);
                    balance += profit;
                    inv.lastProfitDate = today;
                    inv.collectedProfit = (inv.collectedProfit || 0) + profit;
                    changed = true;
                }
            }
        });
        if (changed) {
            setBalance(balance);
            setInvestments(investments);
        }
    }

    // ========== KIỂM TRA ĐIỂM DANH ==========
    function updateCheckinButton() {
        const last = getData('lastCheckin');
        const today = todayStr();
        const btn = document.getElementById('checkin-btn');
        const status = document.getElementById('checkin-status');
        if (last === today) {
            btn.disabled = true;
            btn.textContent = '✅ Đã điểm danh hôm nay';
            status.textContent = 'Bạn đã nhận 1.000đ hôm nay.';
        } else {
            btn.disabled = false;
            btn.textContent = '✅ Điểm danh (+1.000đ)';
            status.textContent = '';
        }
    }

    // ========== HIỂN THỊ SỐ DƯ ==========
    function updateBalanceDisplay() {
        document.getElementById('balance-display').textContent = formatCurrency(getBalance());
    }

    // ========== TẠO GÓI ĐẦU TƯ ==========
    let selectedPackage = null;
    function renderPackages() {
        const container = document.getElementById('package-list');
        container.innerHTML = '';
        PACKAGES.forEach((pkg, index) => {
            const div = document.createElement('div');
            div.className = 'fruit-card';
            div.innerHTML = `<span class="fruit-emoji">${pkg.emoji}</span>
                             <div style="font-size:14px; font-weight:bold;">${pkg.name}</div>
                             <div style="font-size:13px;">${formatCurrency(pkg.amount)}</div>
                             <div style="font-size:12px; color:#2e7d32;">Lãi ${Math.round(pkg.rate*100)}%/ngày</div>`;
            div.onclick = () => {
                document.querySelectorAll('.fruit-card').forEach(c => c.classList.remove('selected'));
                div.classList.add('selected');
                selectedPackage = index;
            };
            container.appendChild(div);
        });
    }

    // ========== ĐẦU TƯ ==========
    function invest() {
        if (selectedPackage === null) { tg.showAlert('Vui lòng chọn gói đầu tư!'); return; }
        const pkg = PACKAGES[selectedPackage];
        const balance = getBalance();
        if (balance < pkg.amount) { tg.showAlert('Số dư không đủ!'); return; }
        // Xác định ngày bắt đầu tính lãi
        const now = new Date();
        const hour = now.getHours();
        let startDate;
        if (hour >= 6 && hour < 18) {
            startDate = addDays(todayStr(), 1);
        } else {
            startDate = addDays(todayStr(), 2);
        }
        // Tạo khoản đầu tư
        const inv = {
            id: Date.now(),
            packageIndex: selectedPackage,
            amount: pkg.amount,
            rate: pkg.rate,
            startDate: startDate,
            lastProfitDate: startDate,
            collectedProfit: 0
        };
        const investments = getInvestments();
        investments.push(inv);
        setInvestments(investments);
        setBalance(balance - pkg.amount);
        updateBalanceDisplay();
        document.getElementById('investment-status').innerText = `Đã đầu tư ${pkg.name} (${formatCurrency(pkg.amount)}), lãi bắt đầu từ ${new Date(startDate).toLocaleDateString('vi-VN')}`;
        selectedPackage = null;
        document.querySelectorAll('.fruit-card').forEach(c => c.classList.remove('selected'));
    }

    // ========== RÚT TIỀN ==========
    function withdraw() {
        const last = getData('lastWithdrawalDate');
        const today = todayStr();
        if (last === today) { tg.showAlert('Mỗi ngày chỉ rút được 1 lần!'); return; }
        const amount = parseInt(document.getElementById('withdraw-amount').value);
        if (!amount || amount < 20000) { tg.showAlert('Tối thiểu 20.000đ'); return; }
        let feePercent;
        if (amount >= 100000) feePercent = 0.07;
        else if (amount >= 50000) feePercent = 0.05;
        else feePercent = 0.02;
        const fee = Math.floor(amount * feePercent);
        const receive = amount - fee;
        const balance = getBalance();
        if (balance < amount) { tg.showAlert('Số dư không đủ'); return; }
        if (receive < 20000) { tg.showAlert('Sau phí nhận dưới 20k, không hợp lệ'); return; }
        setBalance(balance - amount);
        setData('lastWithdrawalDate', today);
        updateBalanceDisplay();
        document.getElementById('withdraw-status').innerText = `Đã rút ${formatCurrency(amount)}, nhận được ${formatCurrency(receive)} (phí ${feePercent*100}%)`;
    }

    // ========== NẠP TIỀN (DEMO) ==========
    function showDepositModal() {
        document.getElementById('deposit-modal').classList.remove('hidden');
    }
    function hideDepositModal() {
        document.getElementById('deposit-modal').classList.add('hidden');
    }
    function confirmDeposit() {
        const amount = parseInt(document.getElementById('deposit-amount-input').value);
        if (!amount || amount <= 0) { tg.showAlert('Nhập số tiền hợp lệ'); return; }
        const now = new Date();
        const hour = now.getHours();
        let note = '';
        if (hour >= 6 && hour < 18) note = 'Lãi sẽ được tính từ ngày mai.';
        else note = 'Nạp sau 18h, lãi tính từ ngày kia.';
        setBalance(getBalance() + amount);
        updateBalanceDisplay();
        tg.showAlert('Nạp thành công ' + formatCurrency(amount) + '. ' + note);
        hideDepositModal();
    }

    // ========== GIỚI THIỆU ==========
    function copyRefLink() {
        const refCode = userId; // dùng chính ID làm mã mời
        const link = `https://t.me/${botUsername}?start=${refCode}`; // cần bot username
        // Vì không biết username bot, ta tạo link tạm
        const fakeLink = `https://t.me/YOUR_BOT?start=${refCode}`;
        tg.writeText(fakeLink);
        tg.showAlert('Link giới thiệu đã được sao chép (thay YOUR_BOT bằng username bot thật)');
    }

    // ========== HIỂN THỊ BẢNG XẾP HẠNG (GIẢ) ==========
    function renderLeaderboard() {
        const list = document.getElementById('leaderboard-list');
        const fakeUsers = [
            { name: 'Alice', profit: 1250000 },
            { name: 'Bob', profit: 980000 },
            { name: 'Carol', profit: 870000 },
            { name: 'Dave', profit: 760000 },
            { name: 'Eve', profit: 650000 },
            { name: 'Frank', profit: 540000 },
            { name: 'Grace', profit: 430000 },
            { name: 'Hank', profit: 320000 },
            { name: 'Ivy', profit: 210000 },
            { name: 'Jack', profit: 150000 }
        ];
        list.innerHTML = fakeUsers.map((u,i) => `
            <div class="rank-item">
                <div class="rank-number">#${i+1}</div>
                <div style="flex:1; font-weight:bold;">${u.name}</div>
                <div style="color:#2e7d32;">+${formatCurrency(u.profit)}</div>
            </div>
        `).join('');
    }

    // ========== HIỂN THỊ ĐỘI NHÓM (GIẢ) ==========
    function renderTeam() {
        const list = document.getElementById('team-list');
        // Lấy số lượng ref giả lập
        const refs = getData('refs') || [];
        if (refs.length === 0) {
            list.innerHTML = '<p style="color:#888;">Bạn chưa có người giới thiệu nào. Hãy mời bạn bè!</p>';
            return;
        }
        list.innerHTML = refs.map(r => `
            <div class="team-card">
                <span>🌿 ${r.name} (ID: ${r.id})</span>
                <span style="float:right;">Lãi: ${formatCurrency(r.profit || 0)} → Bạn nhận ${formatCurrency(Math.floor((r.profit||0)*0.15))}</span>
            </div>
        `).join('');
    }

    // ========== CHUYỂN TAB ==========
    function switchPage(pageId) {
        document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
        document.getElementById(`page-${pageId}`).classList.add('active');
        document.querySelectorAll('.tab-item').forEach(t => t.classList.remove('active'));
        document.querySelector(`.tab-item[data-page="${pageId}"]`).classList.add('active');
    }

    // ========== KHỞI TẠO ==========
    function init() {
        updateAllProfits();
        updateBalanceDisplay();
        updateCheckinButton();
        renderPackages();
        renderLeaderboard();
        renderTeam();
        // Xử lý tham số start (giới thiệu)
        if (tg.initDataUnsafe?.start_param) {
            const refId = tg.initDataUnsafe.start_param;
            // Ghi nhận người giới thiệu
            let refs = getData('refs') || [];
            if (!refs.some(r => r.id === refId)) {
                // Tự thêm ref vào danh sách (giả lập)
                refs.push({ id: refId, name: 'Người giới thiệu ' + refId, profit: 0 });
                setData('refs', refs);
                // Thưởng 2k cho người được ref? (yêu cầu: mời ref 2k 1 ref)
                setBalance(getBalance() + 2000);
                tg.showAlert('Bạn được giới thiệu bởi ' + refId + '. Nhận 2.000đ thưởng.');
                updateBalanceDisplay();
            }
        }
    }

    // ========== SỰ KIỆN ==========
    document.getElementById('checkin-btn').addEventListener('click', () => {
        const last = getData('lastCheckin');
        if (last === todayStr()) return;
        setData('lastCheckin', todayStr());
        setBalance(getBalance() + 1000);
        updateBalanceDisplay();
        updateCheckinButton();
        tg.showAlert('Điểm danh thành công! +1.000đ');
    });

    document.getElementById('invest-btn').addEventListener('click', invest);
    document.getElementById('withdraw-btn').addEventListener('click', withdraw);
    document.getElementById('deposit-btn').addEventListener('click', showDepositModal);
    document.getElementById('confirm-deposit').addEventListener('click', confirmDeposit);
    document.getElementById('close-deposit').addEventListener('click', hideDepositModal);
    document.getElementById('copy-ref-link').addEventListener('click', copyRefLink);

    document.querySelectorAll('.tab-item').forEach(tab => {
        tab.addEventListener('click', () => {
            switchPage(tab.dataset.page);
        });
    });

    // Cập nhật lại lãi mỗi khi mở app
    init();
    setInterval(() => {
        updateAllProfits();
        updateBalanceDisplay();
    }, 60000); // mỗi phút

    // Bot username placeholder (thay bằng username thật của bạn)
    const botUsername = 'supergardening_bot';
</script>
</body>
</html>
