
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cs-Case</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }

        :root {
            --bg: #0f0f13;
            --bg2: #16161d;
            --bg3: #1e1e28;
            --accent: #e8a020;
            --accent2: #c4861a;
            --text: #e0e0e0;
            --text2: #888;
            --red: #eb4b4b;
            --green: #6fcf6f;
            --blue: #4b69ff;
            --purple: #8847ff;
            --pink: #d32ce6;
            --gold: #e4ae33;
        }

        body {
            background: var(--bg);
            color: var(--text);
            font-family: 'Segoe UI', Tahoma, sans-serif;
            min-height: 100vh;
        }

        /* ШАПКА */
        header {
            background: var(--bg2);
            border-bottom: 2px solid #222230;
            padding: 0 30px;
            height: 62px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            position: sticky;
            top: 0;
            z-index: 100;
        }

        .logo {
            font-size: 23px;
            font-weight: 800;
            color: var(--accent);
            letter-spacing: 1px;
            user-select: none;
        }
        .logo span { color: #fff; }

        .header-right {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .balance-badge {
            background: var(--bg3);
            border: 1px solid #2a2a3a;
            padding: 8px 18px;
            border-radius: 20px;
            font-size: 15px;
            font-weight: 700;
            color: var(--accent);
            display: none;
        }

        .username-badge {
            color: var(--text2);
            font-size: 14px;
            display: none;
        }

        .btn-logout {
            background: none;
            border: 1px solid #333;
            color: var(--text2);
            padding: 7px 16px;
            border-radius: 7px;
            cursor: pointer;
            font-size: 13px;
            transition: all .2s;
            display: none;
        }
        .btn-logout:hover { border-color: var(--red); color: var(--red); }

        /* НАВИГАЦИЯ */
        .main-nav {
            display: none;
            gap: 4px;
        }

        .nav-btn {
            background: none;
            border: none;
            color: var(--text2);
            padding: 9px 18px;
            border-radius: 7px;
            cursor: pointer;
            font-size: 14px;
            transition: all .2s;
        }
        .nav-btn:hover { background: var(--bg3); color: var(--text); }
        .nav-btn.active { background: var(--bg3); color: var(--text); }

        /* СТРАНИЦЫ */
        .page { display: none; }
        .page.active { display: block; }

        /* АВТОРИЗАЦИЯ */
        #page-auth {
            min-height: calc(100vh - 62px);
            display: flex;
            align-items: center;
            justify-content: center;
            background: radial-gradient(ellipse at 50% 0%, #1e1e3a 0%, var(--bg) 65%);
        }
        #page-auth.active { display: flex; }

        .auth-wrap { width: 390px; }

        .auth-logo-big {
            text-align: center;
            font-size: 30px;
            font-weight: 800;
            color: var(--accent);
            margin-bottom: 6px;
        }
        .auth-logo-big span { color: #fff; }

        .auth-desc {
            text-align: center;
            color: var(--text2);
            font-size: 13px;
            margin-bottom: 24px;
        }

        .auth-box {
            background: var(--bg2);
            border: 1px solid #252535;
            border-radius: 14px;
            padding: 30px;
        }

        .auth-tabs {
            display: flex;
            background: var(--bg3);
            border-radius: 9px;
            padding: 4px;
            margin-bottom: 24px;
        }

        .auth-tab {
            flex: 1;
            background: none;
            border: none;
            color: var(--text2);
            padding: 10px;
            border-radius: 7px;
            cursor: pointer;
            font-size: 14px;
            font-weight: 600;
            transition: all .2s;
        }
        .auth-tab.active {
            background: var(--accent);
            color: #000;
        }

        .auth-form { display: none; }
        .auth-form.active { display: block; }

        .form-group { margin-bottom: 15px; }
        .form-group label {
            display: block;
            font-size: 12px;
            color: var(--text2);
            margin-bottom: 6px;
            text-transform: uppercase;
            letter-spacing: .5px;
        }
        .form-group input {
            width: 100%;
            background: var(--bg3);
            border: 1px solid #252535;
            border-radius: 8px;
            padding: 12px 14px;
            color: var(--text);
            font-size: 14px;
            outline: none;
            transition: border .2s;
        }
        .form-group input:focus { border-color: var(--accent); }

        .btn-auth {
            width: 100%;
            background: var(--accent);
            color: #000;
            border: none;
            padding: 13px;
            border-radius: 9px;
            font-size: 15px;
            font-weight: 700;
            cursor: pointer;
            transition: background .2s;
            margin-top: 4px;
        }
        .btn-auth:hover { background: var(--accent2); }

        .bonus-hint {
            text-align: center;
            margin-top: 14px;
            font-size: 12px;
            color: var(--text2);
        }
        .bonus-hint b { color: var(--accent); }

        .err-box {
            background: rgba(235,75,75,.12);
            border: 1px solid rgba(235,75,75,.35);
            color: var(--red);
            padding: 10px 14px;
            border-radius: 8px;
            font-size: 13px;
            margin-bottom: 14px;
            display: none;
        }

        /* ОСНОВНОЕ */
        .content {
            max-width: 1200px;
            margin: 0 auto;
            padding: 28px 20px;
        }

        .tabs-row {
            display: flex;
            gap: 4px;
            background: var(--bg2);
            border: 1px solid #252535;
            border-radius: 9px;
            padding: 4px;
            width: fit-content;
            margin-bottom: 26px;
        }

        .tab-btn {
            background: none;
            border: none;
            color: var(--text2);
            padding: 9px 22px;
            border-radius: 7px;
            cursor: pointer;
            font-size: 14px;
            transition: all .2s;
        }
        .tab-btn.active {
            background: var(--bg3);
            color: var(--text);
            font-weight: 600;
        }

        /* БАННЕР */
        .welcome-banner {
            background: linear-gradient(135deg, #1c1c30, #151525);
            border: 1px solid rgba(232,160,32,.25);
            border-radius: 12px;
            padding: 22px 28px;
            margin-bottom: 28px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            gap: 20px;
        }
        .welcome-banner h3 { font-size: 17px; margin-bottom: 5px; }
        .welcome-banner p { color: var(--text2); font-size: 13px; }
        .banner-sum {
            font-size: 32px;
            font-weight: 800;
            color: var(--accent);
            white-space: nowrap;
        }

        /* КЕЙСЫ */
        .section-title {
            font-size: 19px;
            font-weight: 700;
            margin-bottom: 5px;
        }
        .section-sub {
            color: var(--text2);
            font-size: 13px;
            margin-bottom: 22px;
        }

        .cases-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(175px, 1fr));
            gap: 14px;
        }

        .case-card {
            background: var(--bg2);
            border: 1px solid #252535;
            border-radius: 11px;
            overflow: hidden;
            cursor: pointer;
            transition: transform .2s, border-color .2s;
        }
        .case-card:hover {
            transform: translateY(-4px);
            border-color: var(--accent);
        }

        .case-img {
            height: 130px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 54px;
            position: relative;
        }

        .case-badge {
            position: absolute;
            top: 8px;
            right: 8px;
            background: rgba(0,0,0,.6);
            border-radius: 5px;
            padding: 2px 7px;
            font-size: 11px;
            color: var(--accent);
            font-weight: 700;
        }

        .case-info { padding: 12px; }
        .case-name {
            font-size: 13px;
            font-weight: 600;
            margin-bottom: 9px;
            line-height: 1.3;
        }
        .case-price-row {
            display: flex;
            align-items: center;
            justify-content: space-between;
        }
        .case-price {
            color: var(--accent);
            font-weight: 700;
            font-size: 16px;
        }
        .case-open-btn {
            background: var(--accent);
            color: #000;
            border: none;
            padding: 5px 12px;
            border-radius: 6px;
            font-size: 12px;
            font-weight: 700;
            cursor: pointer;
        }

        /* МОДАЛКА */
        .overlay {
            position: fixed;
            inset: 0;
            background: rgba(0,0,0,.88);
            z-index: 200;
            display: none;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }
        .overlay.show { display: flex; }

        .modal {
            background: var(--bg2);
            border: 1px solid #252535;
            border-radius: 14px;
            padding: 28px;
            width: 680px;
            max-width: 100%;
            text-align: center;
        }

        .modal-title { font-size: 20px; font-weight: 700; margin-bottom: 4px; }
        .modal-sub { color: var(--text2); font-size: 13px; margin-bottom: 20px; }

        /* РУЛЕТКА */
        .roulette-outer {
            position: relative;
            overflow: hidden;
            border: 2px solid #252535;
            border-radius: 9px;
            height: 135px;
            margin-bottom: 20px;
            background: var(--bg3);
        }

        .roulette-line {
            position: absolute;
            top: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 3px;
            height: 100%;
            background: var(--accent);
            z-index: 10;
            pointer-events: none;
        }
        .roulette-line::before {
            content: '';
            position: absolute;
            top: 0;
            left: 50%;
            transform: translateX(-50%);
            border: 9px solid transparent;
            border-top: 14px solid var(--accent);
        }
        .roulette-line::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 50%;
            transform: translateX(-50%);
            border: 9px solid transparent;
            border-bottom: 14px solid var(--accent);
        }

        .roulette-track {
            display: flex;
            gap: 6px;
            padding: 8px;
            will-change: transform;
        }

        .r-item {
            min-width: 112px;
            width: 112px;
            height: 117px;
            border-radius: 8px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            flex-shrink: 0;
            border: 2px solid transparent;
            padding: 6px;
            gap: 4px;
        }
        .r-item-icon { font-size: 30px; }
        .r-item-name {
            font-size: 9px;
            font-weight: 600;
            line-height: 1.3;
            text-align: center;
            max-width: 100px;
        }

        /* РЕЗУЛЬТАТ */
        .result-wrap {
            margin-bottom: 18px;
            display: none;
        }
        .result-wrap.show { display: block; }

        .result-card-big {
            display: inline-flex;
            flex-direction: column;
            align-items: center;
            border-radius: 12px;
            padding: 20px 36px;
            border: 2px solid;
            gap: 6px;
        }
        .result-icon { font-size: 58px; }
        .result-name { font-size: 16px; font-weight: 700; }
        .result-rarity-label { font-size: 12px; }
        .result-val { font-size: 20px; font-weight: 800; color: var(--accent); }

        /* КНОПКИ МОДАЛКИ */
        .modal-btns {
            display: flex;
            gap: 10px;
            justify-content: center;
            flex-wrap: wrap;
        }

        .btn-do-open {
            background: var(--accent);
            color: #000;
            border: none;
            padding: 12px 30px;
            border-radius: 9px;
            font-size: 15px;
            font-weight: 700;
            cursor: pointer;
            transition: background .2s;
        }
        .btn-do-open:hover { background: var(--accent2); }
        .btn-do-open:disabled { opacity: .5; cursor: not-allowed; }

        .btn-sell-win {
            background: #1a3a1a;
            color: var(--green);
            border: 1px solid #2a5a2a;
            padding: 12px 24px;
            border-radius: 9px;
            font-size: 14px;
            font-weight: 600;
            cursor: pointer;
            transition: all .2s;
            display: none;
        }
        .btn-sell-win:hover { background: #234a23; }
        .btn-sell-win.show { display: block; }

        .btn-keep-win {
            background: var(--bg3);
            color: var(--text);
            border: 1px solid #2a2a3a;
            padding: 12px 24px;
            border-radius: 9px;
            font-size: 14px;
            cursor: pointer;
            transition: all .2s;
            display: none;
        }
        .btn-keep-win:hover { border-color: #555; }
        .btn-keep-win.show { display: block; }

        .btn-modal-close {
            background: var(--bg3);
            color: var(--text2);
            border: 1px solid #252535;
            padding: 12px 24px;
            border-radius: 9px;
            font-size: 14px;
            cursor: pointer;
            transition: all .2s;
        }
        .btn-modal-close:hover { color: var(--text); border-color: #444; }

        .no-bal-msg {
            color: var(--red);
            font-size: 13px;
            margin-bottom: 14px;
            display: none;
        }
        .no-bal-msg.show { display: block; }

        /* ИНВЕНТАРЬ */
        .inv-header {
            display: flex;
            align-items: flex-start;
            justify-content: space-between;
            margin-bottom: 20px;
            gap: 16px;
            flex-wrap: wrap;
        }

        .inv-stats {
            display: flex;
            gap: 12px;
            flex-wrap: wrap;
        }

        .inv-stat {
            background: var(--bg2);
            border: 1px solid #252535;
            border-radius: 9px;
            padding: 12px 20px;
            text-align: center;
            min-width: 100px;
        }
        .inv-stat .v {
            font-size: 20px;
            font-weight: 800;
            color: var(--accent);
        }
        .inv-stat .l {
            font-size: 11px;
            color: var(--text2);
            margin-top: 2px;
        }

        .withdraw-info {
            background: rgba(75,105,255,.08);
            border: 1px solid rgba(75,105,255,.25);
            border-radius: 8px;
            padding: 11px 16px;
            font-size: 13px;
            color: #8899ee;
            margin-bottom: 20px;
        }

        .inv-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(145px, 1fr));
            gap: 12px;
        }

        .inv-card {
            background: var(--bg2);
            border: 1px solid #252535;
            border-radius: 11px;
            overflow: hidden;
        }

        .inv-card-img {
            height: 105px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 38px;
        }

        .inv-card-info { padding: 10px; }
        .inv-card-name {
            font-size: 11px;
            font-weight: 600;
            line-height: 1.3;
            margin-bottom: 4px;
        }
        .inv-card-val {
            font-size: 14px;
            font-weight: 700;
            color: var(--accent);
            margin-bottom: 9px;
        }
        .inv-card-rarity {
            font-size: 10px;
            margin-bottom: 8px;
        }

        .inv-card-btns { display: flex; gap: 5px; }

        .btn-inv-sell {
            flex: 1;
            background: #1a3a1a;
            color: var(--green);
            border: 1px solid #2a5a2a;
            padding: 6px 4px;
            border-radius: 6px;
            font-size: 11px;
            font-weight: 600;
            cursor: pointer;
            transition: all .2s;
        }
        .btn-inv-sell:hover { background: #254a25; }

        .btn-inv-withdraw {
            flex: 1;
            background: #1a1a3a;
            color: #8899ee;
            border: 1px solid #2a2a5a;
            padding: 6px 4px;
            border-radius: 6px;
            font-size: 11px;
            font-weight: 600;
            cursor: pointer;
            transition: all .2s;
        }
        .btn-inv-withdraw:hover { background: #252550; }
        .btn-inv-withdraw:disabled {
            opacity: .35;
            cursor: not-allowed;
        }

        .inv-empty {
            grid-column: 1/-1;
            text-align: center;
            padding: 70px 0;
            color: var(--text2);
        }
        .inv-empty div:first-child { font-size: 50px; margin-bottom: 14px; }

        /* ТОСТ */
        .toast {
            position: fixed;
            bottom: 28px;
            right: 28px;
            background: var(--bg2);
            border: 1px solid #252535;
            border-radius: 11px;
            padding: 14px 20px;
            font-size: 14px;
            z-index: 999;
            max-width: 290px;
            line-height: 1.4;
            transform: translateY(90px);
            opacity: 0;
            transition: all .3s;
            pointer-events: none;
        }
        .toast.show { transform: translateY(0); opacity: 1; }
        .toast.t-green { border-color: #2a5a2a; color: var(--green); }
        .toast.t-orange { border-color: var(--accent2); color: var(--accent); }
        .toast.t-red { border-color: #5a2a2a; color: var(--red); }
        .toast.t-blue { border-color: #2a2a5a; color: #8899ee; }

        /* Редкости - цвета фонов */
        .rarity-consumer    { background: rgba(176,176,176,.1); border-color: #b0b0b0 !important; }
        .rarity-industrial  { background: rgba(94,152,217,.1); border-color: #5e98d9 !important; }
        .rarity-milspec     { background: rgba(75,105,255,.1); border-color: #4b69ff !important; }
        .rarity-restricted  { background: rgba(136,71,255,.1); border-color: #8847ff !important; }
        .rarity-classified  { background: rgba(211,44,230,.1); border-color: #d32ce6 !important; }
        .rarity-covert      { background: rgba(235,75,75,.1); border-color: #eb4b4b !important; }
        .rarity-contraband  { background: rgba(228,174,51,.15); border-color: #e4ae33 !important; }

        .rl-consumer    { color: #b0b0b0; }
        .rl-industrial  { color: #5e98d9; }
        .rl-milspec     { color: #4b69ff; }
        .rl-restricted  { color: #8847ff; }
        .rl-classified  { color: #d32ce6; }
        .rl-covert      { color: #eb4b4b; }
        .rl-contraband  { color: #e4ae33; }

        @media(max-width:600px){
            .welcome-banner { flex-direction: column; text-align: center; }
            .cases-grid { grid-template-columns: repeat(auto-fill, minmax(140px,1fr)); }
            .inv-grid { grid-template-columns: repeat(auto-fill, minmax(130px,1fr)); }
            .modal { padding: 20px 14px; }
        }
    </style>
</head>
<body>

<!-- ШАПКА -->
<header>
    <div class="logo">Cs<span>-Case</span></div>
    <div class="main-nav" id="main-nav">
        <button class="nav-btn active" onclick="showTab('cases')">🎁 Кейсы</button>
        <button class="nav-btn" onclick="showTab('inventory')">🎒 Инвентарь</button>
    </div>
    <div class="header-right">
        <span class="username-badge" id="username-badge"></span>
        <div class="balance-badge" id="balance-badge">💰 <span id="bal-num">0</span> ₽</div>
        <button class="btn-logout" id="btn-logout" onclick="logout()">Выйти</button>
    </div>
</header>

<!-- СТРАНИЦА АВТОРИЗАЦИИ -->
<div class="page active" id="page-auth">
    <div class="auth-wrap">
        <div class="auth-logo-big">Cs<span>-Case</span></div>
        <div class="auth-desc">Открывай кейсы CS2 и получай крутые скины</div>
        <div class="auth-box">
            <div class="auth-tabs">
                <button class="auth-tab active" onclick="switchAuthTab('login')">Войти</button>
                <button class="auth-tab" onclick="switchAuthTab('register')">Регистрация</button>
            </div>
            <div class="err-box" id="auth-err"></div>

            <!-- Вход -->
            <div class="auth-form active" id="form-login">
                <div class="form-group">
                    <label>Логин</label>
                    <input type="text" id="inp-login" placeholder="Введи логин" onkeydown="if(event.key==='Enter')doLogin()">
                </div>
                <div class="form-group">
                    <label>Пароль</label>
                    <input type="password" id="inp-pass" placeholder="Введи пароль" onkeydown="if(event.key==='Enter')doLogin()">
                </div>
                <button class="btn-auth" onclick="doLogin()">Войти</button>
            </div>

            <!-- Регистрация -->
            <div class="auth-form" id="form-register">
                <div class="form-group">
                    <label>Логин</label>
                    <input type="text" id="inp-reg-login" placeholder="Придумай логин" onkeydown="if(event.key==='Enter')doRegister()">
                </div>
                <div class="form-group">
                    <label>Пароль</label>
                    <input type="password" id="inp-reg-pass" placeholder="Придумай пароль" onkeydown="if(event.key==='Enter')doRegister()">
                </div>
                <div class="form-group">
                    <label>Повтори пароль</label>
                    <input type="password" id="inp-reg-pass2" placeholder="Ещё раз пароль" onkeydown="if(event.key==='Enter')doRegister()">
                </div>
                <button class="btn-auth" onclick="doRegister()">Зарегаться</button>
                <div class="bonus-hint">При регистрации получишь <b>150 ₽</b> бесплатно 🎉</div>
            </div>
        </div>
    </div>
</div>

<!-- ГЛАВНАЯ СТРАНИЦА -->
<div class="page" id="page-main">
    <div class="content">
        <div class="tabs-row">
            <button class="tab-btn active" id="tab-cases" onclick="showTab('cases')">🎁 Кейсы</button>
            <button class="tab-btn" id="tab-inventory" onclick="showTab('inventory')">🎒 Инвентарь</button>
        </div>

        <!-- ВКЛАДКА КЕЙСЫ -->
        <div id="section-cases">
            <div class="welcome-banner" id="welcome-banner">
                <div>
                    <h3 id="welcome-name">Привет! 👋</h3>
                    <p>На старт тебе дали 150 ₽ — открывай кейсы!</p>
                </div>
                <div class="banner-sum">150 ₽</div>
            </div>
            <div class="section-title">Все кейсы</div>
            <div class="section-sub">Нажми на кейс чтобы открыть</div>
            <div class="cases-grid" id="cases-grid"></div>
        </div>

        <!-- ВКЛАДКА ИНВЕНТАРЬ -->
        <div id="section-inventory" style="display:none">
            <div class="inv-header">
                <div>
                    <div class="section-title">Мой инвентарь</div>
                    <div class="section-sub">Скины которые ты выбил</div>
                </div>
                <div class="inv-stats">
                    <div class="inv-stat">
                        <div class="v" id="stat-count">0</div>
                        <div class="l">Скинов</div>
                    </div>
                    <div class="inv-stat">
                        <div class="v" id="stat-total">0 ₽</div>
                        <div class="l">Стоимость</div>
                    </div>
                    <div class="inv-stat">
                        <div class="v" id="stat-withdrawn">0/10</div>
                        <div class="l">Выведено</div>
                    </div>
                </div>
            </div>
            <div class="withdraw-info">
                ℹ️ Вывод скинов доступен до 10 штук. Дальше только продажа за рубли.
            </div>
            <div class="inv-grid" id="inv-grid"></div>
        </div>
    </div>
</div>

<!-- МОДАЛКА КЕЙСА -->
<div class="overlay" id="case-overlay">
    <div class="modal">
        <div class="modal-title" id="m-case-name">Кейс</div>
        <div class="modal-sub" id="m-case-sub">Цена: 75 ₽</div>
        <div class="roulette-outer">
            <div class="roulette-line"></div>
            <div class="roulette-track" id="r-track"></div>
        </div>
        <div class="no-bal-msg" id="no-bal-msg">Не хватает баланса для открытия 😔</div>
        <div class="result-wrap" id="result-wrap">
            <div class="result-card-big" id="result-card">
                <div class="result-icon" id="res-icon">🔫</div>
                <div class="result-name" id="res-name">AK-47 | Redline</div>
                <div class="result-rarity-label" id="res-rarity">Classified</div>
                <div class="result-val" id="res-val">1200 ₽</div>
            </div>
        </div>
        <div class="modal-btns">
            <button class="btn-do-open" id="btn-do-open" onclick="openCase()">🔓 Открыть</button>
            <button class="btn-sell-win" id="btn-sell-win" onclick="sellWon()">💰 Продать</button>
            <button class="btn-keep-win" id="btn-keep-win" onclick="keepWon()">🎒 В инвентарь</button>
            <button class="btn-modal-close" onclick="closeModal()">Закрыть</button>
        </div>
    </div>
</div>

<!-- ТОСТ -->
<div class="toast" id="toast"></div>
<script>
// ===================== ДАННЫЕ КЕЙСОВ =====================

const CASES = [
    {
        id: 1, name: "Starter Case", price: 49, emoji: "📦",
        bg: "linear-gradient(135deg,#1a2a1a,#2a3a2a)",
        skins: [
            { name:"Glock-18 | Groundwater",      rarity:"consumer",    value:12,  emoji:"🔫", chance:30 },
            { name:"MP9 | Hot Rod",                rarity:"consumer",    value:18,  emoji:"🔫", chance:25 },
            { name:"P250 | Sand Dune",             rarity:"industrial",  value:40,  emoji:"🔫", chance:18 },
            { name:"FAMAS | Doomkitty",            rarity:"milspec",     value:95,  emoji:"🔫", chance:12 },
            { name:"AUG | Torque",                 rarity:"milspec",     value:130, emoji:"🔫", chance:8  },
            { name:"M4A1-S | Bright Water",        rarity:"restricted",  value:290, emoji:"🔫", chance:4  },
            { name:"AK-47 | Safari Mesh",          rarity:"classified",  value:720, emoji:"🔫", chance:2  },
            { name:"AWP | Asiimov",                rarity:"covert",      value:3400,emoji:"🔫", chance:1  },
        ]
    },
    {
        id: 2, name: "Chroma Case", price: 75, emoji: "🟣",
        bg: "linear-gradient(135deg,#1a1040,#2a1a60)",
        skins: [
            { name:"Nova | Tornado",               rarity:"consumer",    value:14,  emoji:"🔫", chance:30 },
            { name:"Five-SeveN | Kami",            rarity:"consumer",    value:22,  emoji:"🔫", chance:25 },
            { name:"G3SG1 | Polar Bear",           rarity:"industrial",  value:50,  emoji:"🔫", chance:18 },
            { name:"SSG 08 | Abyss",               rarity:"milspec",     value:115, emoji:"🔫", chance:12 },
            { name:"P90 | Trigon",                 rarity:"milspec",     value:145, emoji:"🔫", chance:8  },
            { name:"Galil AR | Chatterbox",        rarity:"restricted",  value:340, emoji:"🔫", chance:4  },
            { name:"M4A4 | Dragon King",           rarity:"classified",  value:1150,emoji:"🔫", chance:2  },
            { name:"AK-47 | Vulcan",               rarity:"covert",      value:8800,emoji:"🔫", chance:1  },
        ]
    },
    {
        id: 3, name: "Danger Zone Case", price: 85, emoji: "⚠️",
        bg: "linear-gradient(135deg,#3a1010,#5a2020)",
        skins: [
            { name:"P2000 | Urban Hazard",         rarity:"consumer",    value:16,  emoji:"🔫", chance:30 },
            { name:"MAC-10 | Pipe Down",           rarity:"consumer",    value:24,  emoji:"🔫", chance:25 },
            { name:"XM1014 | Irezumi",             rarity:"industrial",  value:55,  emoji:"🔫", chance:18 },
            { name:"MP5-SD | Agent",               rarity:"milspec",     value:135, emoji:"🔫", chance:12 },
            { name:"Sawed-Off | Apocalypto",       rarity:"milspec",     value:160, emoji:"🔫", chance:8  },
            { name:"M4A1-S | Flashback",           rarity:"restricted",  value:470, emoji:"🔫", chance:4  },
            { name:"Desert Eagle | Printstream",   rarity:"classified",  value:2900,emoji:"🔫", chance:2  },
            { name:"AWP | Neo-Noir",               rarity:"covert",      value:6400,emoji:"🔫", chance:1  },
        ]
    },
    {
        id: 4, name: "Prisma Case", price: 90, emoji: "💎",
        bg: "linear-gradient(135deg,#0a1a3a,#1a2a5a)",
        skins: [
            { name:"MP9 | Hydra",                  rarity:"consumer",    value:18,  emoji:"🔫", chance:30 },
            { name:"P250 | Verdigris",             rarity:"consumer",    value:26,  emoji:"🔫", chance:25 },
            { name:"Tec-9 | Bamboozle",            rarity:"industrial",  value:60,  emoji:"🔫", chance:18 },
            { name:"SG 553 | Phantasm",            rarity:"milspec",     value:150, emoji:"🔫", chance:12 },
            { name:"UMP-45 | Primal Saber",        rarity:"milspec",     value:180, emoji:"🔫", chance:8  },
            { name:"Glock-18 | Twilight Galaxy",   rarity:"restricted",  value:540, emoji:"🔫", chance:4  },
            { name:"AUG | Momentum",               rarity:"classified",  value:1900,emoji:"🔫", chance:2  },
            { name:"M4A1-S | Player Two",          rarity:"covert",      value:4700,emoji:"🔫", chance:1  },
        ]
    },
    {
        id: 5, name: "Fracture Case", price: 95, emoji: "💥",
        bg: "linear-gradient(135deg,#2a1a00,#4a3000)",
        skins: [
            { name:"Nova | Wood Fired",            rarity:"consumer",    value:20,  emoji:"🔫", chance:30 },
            { name:"CZ75-Auto | Vendetta",         rarity:"industrial",  value:62,  emoji:"🔫", chance:25 },
            { name:"MP5-SD | Oxide Oasis",         rarity:"milspec",     value:165, emoji:"🔫", chance:18 },
            { name:"P90 | Neoqueen",               rarity:"milspec",     value:195, emoji:"🔫", chance:12 },
            { name:"Five-SeveN | Angry Mob",       rarity:"restricted",  value:590, emoji:"🔫", chance:8  },
            { name:"AK-47 | Phantom Disruptor",    rarity:"classified",  value:2300,emoji:"🔫", chance:4  },
            { name:"Desert Eagle | Kumicho Dragon",rarity:"classified",  value:2000,emoji:"🔫", chance:2  },
            { name:"M4A4 | Tooth Fairy",           rarity:"covert",      value:8100,emoji:"🔫", chance:1  },
        ]
    },
    {
        id: 6, name: "Snakebite Case", price: 100, emoji: "🐍",
        bg: "linear-gradient(135deg,#0d2a00,#1a4a00)",
        skins: [
            { name:"Sawed-Off | Snake Camo",       rarity:"consumer",    value:22,  emoji:"🔫", chance:30 },
            { name:"MP9 | Venom",                  rarity:"industrial",  value:66,  emoji:"🔫", chance:25 },
            { name:"G3SG1 | Viper",                rarity:"milspec",     value:178, emoji:"🔫", chance:18 },
            { name:"MAC-10 | Allure",              rarity:"milspec",     value:205, emoji:"🔫", chance:12 },
            { name:"M4A1-S | Welcome to Jungle",   rarity:"restricted",  value:650, emoji:"🔫", chance:8  },
            { name:"AK-47 | Slate",                rarity:"classified",  value:2600,emoji:"🔫", chance:4  },
            { name:"UMP-45 | Wild Child",          rarity:"covert",      value:5700,emoji:"🔫", chance:2  },
            { name:"★ Shadow Daggers | Safari Mesh",rarity:"contraband", value:14500,emoji:"🗡️",chance:1  },
        ]
    },
    {
        id: 7, name: "Riptide Case", price: 105, emoji: "🌊",
        bg: "linear-gradient(135deg,#001a3a,#003060)",
        skins: [
            { name:"FAMAS | Crypsis",              rarity:"consumer",    value:24,  emoji:"🔫", chance:30 },
            { name:"XM1014 | Watchdog",            rarity:"industrial",  value:70,  emoji:"🔫", chance:25 },
            { name:"USP-S | Ticket to Hell",       rarity:"milspec",     value:192, emoji:"🔫", chance:18 },
            { name:"CZ75-Auto | Circaetus",        rarity:"milspec",     value:220, emoji:"🔫", chance:12 },
            { name:"Galil AR | Connexion",         rarity:"restricted",  value:720, emoji:"🔫", chance:8  },
            { name:"M4A4 | In Living Color",       rarity:"classified",  value:3200,emoji:"🔫", chance:4  },
            { name:"AWP | Pole Position",          rarity:"covert",      value:9200,emoji:"🔫", chance:2  },
            { name:"★ Falchion Knife | Doppler",   rarity:"contraband",  value:22500,emoji:"🗡️",chance:1  },
        ]
    },
    {
        id: 8, name: "Dreams & Nightmares", price: 110, emoji: "🌙",
        bg: "linear-gradient(135deg,#1a0a2a,#2a1040)",
        skins: [
            { name:"PP-Bizon | Space Cat",         rarity:"consumer",    value:28,  emoji:"🔫", chance:30 },
            { name:"P2000 | Acid Etched",          rarity:"industrial",  value:74,  emoji:"🔫", chance:25 },
            { name:"AUG | Stymphalian",            rarity:"milspec",     value:212, emoji:"🔫", chance:18 },
            { name:"SG 553 | Darkwing",            rarity:"milspec",     value:245, emoji:"🔫", chance:12 },
            { name:"Nova | Sobek",                 rarity:"restricted",  value:780, emoji:"🔫", chance:8  },
            { name:"MP5-SD | Necro Jr.",           rarity:"classified",  value:3600,emoji:"🔫", chance:4  },
            { name:"AK-47 | X-Ray",               rarity:"covert",      value:11500,emoji:"🔫",chance:2  },
            { name:"★ Gut Knife | Marble Fade",    rarity:"contraband",  value:29000,emoji:"🗡️",chance:1  },
        ]
    },
    {
        id: 9, name: "Recoil Case", price: 115, emoji: "💢",
        bg: "linear-gradient(135deg,#3a1500,#5a2500)",
        skins: [
            { name:"Dual Berettas | Flora Carnivora",rarity:"consumer",  value:30,  emoji:"🔫", chance:30 },
            { name:"P250 | Re.built",              rarity:"industrial",  value:78,  emoji:"🔫", chance:25 },
            { name:"MAC-10 | Monkeyflage",         rarity:"milspec",     value:228, emoji:"🔫", chance:18 },
            { name:"FAMAS | Meow 36",              rarity:"milspec",     value:260, emoji:"🔫", chance:12 },
            { name:"Glock-18 | Umbral Rabbit",     rarity:"restricted",  value:840, emoji:"🔫", chance:8  },
            { name:"M4A1-S | Fog of War",          rarity:"classified",  value:4100,emoji:"🔫", chance:4  },
            { name:"AK-47 | Ice Coaled",           rarity:"covert",      value:13000,emoji:"🔫",chance:2  },
            { name:"★ Paracord Knife | Doppler",   rarity:"contraband",  value:31000,emoji:"🗡️",chance:1  },
        ]
    },
    {
        id: 10, name: "Revolution Case", price: 120, emoji: "🔴",
        bg: "linear-gradient(135deg,#2a0000,#500000)",
        skins: [
            { name:"Tec-9 | Rebel",                rarity:"consumer",    value:32,  emoji:"🔫", chance:30 },
            { name:"XM1014 | Zombie Offensive",    rarity:"industrial",  value:82,  emoji:"🔫", chance:25 },
            { name:"MP9 | Starlight Protector",    rarity:"milspec",     value:245, emoji:"🔫", chance:18 },
            { name:"Nova | Toy Soldier",           rarity:"milspec",     value:275, emoji:"🔫", chance:12 },
            { name:"M4A4 | Temukau",               rarity:"restricted",  value:900, emoji:"🔫", chance:8  },
            { name:"Desert Eagle | Blue Ply",      rarity:"classified",  value:4500,emoji:"🔫", chance:4  },
            { name:"AK-47 | Head Shot",            rarity:"covert",      value:15000,emoji:"🔫",chance:2  },
            { name:"★ Stiletto Knife | Tiger Tooth",rarity:"contraband", value:36000,emoji:"🗡️",chance:1  },
        ]
    },
    {
        id: 11, name: "Kilowatt Case", price: 130, emoji: "⚡",
        bg: "linear-gradient(135deg,#1a1a00,#3a3a00)",
        skins: [
            { name:"MP5-SD | Condition Zero",      rarity:"consumer",    value:35,  emoji:"🔫", chance:30 },
            { name:"P250 | Cyber Shell",           rarity:"industrial",  value:88,  emoji:"🔫", chance:25 },
            { name:"AWP | Chrome Cannon",          rarity:"milspec",     value:260, emoji:"🔫", chance:18 },
            { name:"SG 553 | IDC",                 rarity:"milspec",     value:290, emoji:"🔫", chance:12 },
            { name:"AK-47 | Inheritance",          rarity:"restricted",  value:960, emoji:"🔫", chance:8  },
            { name:"USP-S | Jawbreaker",           rarity:"classified",  value:4900,emoji:"🔫", chance:4  },
            { name:"M4A1-S | Emphorosaur-S",       rarity:"covert",      value:17000,emoji:"🔫",chance:2  },
            { name:"★ Talon Knife | Fade",         rarity:"contraband",  value:42000,emoji:"🗡️",chance:1  },
        ]
    },
    {
        id: 12, name: "Gallery Case", price: 140, emoji: "🎨",
        bg: "linear-gradient(135deg,#0a0a2a,#1a102a)",
        skins: [
            { name:"MP9 | Featherweight",          rarity:"consumer",    value:38,  emoji:"🔫", chance:30 },
            { name:"Sawed-Off | Analog Input",     rarity:"industrial",  value:92,  emoji:"🔫", chance:25 },
            { name:"UMP-45 | Plastique",           rarity:"milspec",     value:275, emoji:"🔫", chance:18 },
            { name:"AUG | Plague",                 rarity:"milspec",     value:310, emoji:"🔫", chance:12 },
            { name:"Glock-18 | Block-18",          rarity:"restricted",  value:1050,emoji:"🔫", chance:8  },
            { name:"AK-47 | Uncharted",            rarity:"classified",  value:5400,emoji:"🔫", chance:4  },
            { name:"M4A4 | Etch Lord",             rarity:"covert",      value:19000,emoji:"🔫",chance:2  },
            { name:"★ Butterfly Knife | Lore",     rarity:"contraband",  value:55000,emoji:"🗡️",chance:1  },
        ]
    },
    {
        id: 13, name: "Weapon Case 3", price: 155, emoji: "🎯",
        bg: "linear-gradient(135deg,#001a1a,#003030)",
        skins: [
            { name:"Nova | Antique",               rarity:"consumer",    value:42,  emoji:"🔫", chance:30 },
            { name:"G3SG1 | Orange Kimono",        rarity:"industrial",  value:98,  emoji:"🔫", chance:25 },
            { name:"Galil AR | Rocket Pop",        rarity:"milspec",     value:290, emoji:"🔫", chance:18 },
            { name:"M249 | System Lock",           rarity:"milspec",     value:330, emoji:"🔫", chance:12 },
            { name:"Desert Eagle | Conspiracy",    rarity:"restricted",  value:1150,emoji:"🔫", chance:8  },
            { name:"AK-47 | Fire Serpent",         rarity:"classified",  value:18000,emoji:"🔫",chance:4  },
            { name:"M4A4 | Howl",                  rarity:"contraband",  value:85000,emoji:"🔫",chance:1  },
            { name:"★ Karambit | Autotronic",      rarity:"contraband",  value:62000,emoji:"🗡️",chance:1  },
        ]
    },
    {
        id: 14, name: "Clutch Case", price: 170, emoji: "🏆",
        bg: "linear-gradient(135deg,#1a1500,#302800)",
        skins: [
            { name:"FAMAS | Spitfire",             rarity:"consumer",    value:46,  emoji:"🔫", chance:30 },
            { name:"XM1014 | Black Tie",           rarity:"industrial",  value:105, emoji:"🔫", chance:25 },
            { name:"MP7 | Powercore",              rarity:"milspec",     value:310, emoji:"🔫", chance:18 },
            { name:"P90 | Shallow Grave",          rarity:"milspec",     value:350, emoji:"🔫", chance:12 },
            { name:"Five-SeveN | Hyper Beast",     rarity:"restricted",  value:1350,emoji:"🔫", chance:8  },
            { name:"M4A1-S | Hyper Beast",         rarity:"classified",  value:6800,emoji:"🔫", chance:4  },
            { name:"AWP | Hyper Beast",            rarity:"covert",      value:26000,emoji:"🔫",chance:2  },
            { name:"★ Bowie Knife | Doppler",      rarity:"contraband",  value:38000,emoji:"🗡️",chance:1  },
        ]
    },
    {
        id: 15, name: "Operation Bravo", price: 200, emoji: "🌟",
        bg: "linear-gradient(135deg,#1a0a00,#3a2000)",
        skins: [
            { name:"P250 | Splash",                rarity:"consumer",    value:52,  emoji:"🔫", chance:28 },
            { name:"MP9 | Bulldozer",              rarity:"industrial",  value:115, emoji:"🔫", chance:22 },
            { name:"AUG | Wings",                  rarity:"milspec",     value:340, emoji:"🔫", chance:18 },
            { name:"Desert Eagle | Golden Koi",    rarity:"milspec",     value:390, emoji:"🔫", chance:14 },
            { name:"AK-47 | Jaguar",               rarity:"restricted",  value:1600,emoji:"🔫", chance:8  },
            { name:"M4A4 | Faded Zebra",           rarity:"classified",  value:7500,emoji:"🔫", chance:5  },
            { name:"AWP | Dragon Lore",            rarity:"contraband",  value:120000,emoji:"🔫",chance:2  },
            { name:"★ Karambit | Crimson Web",     rarity:"contraband",  value:95000,emoji:"🗡️",chance:1  },
        ]
    },
];

// Названия редкостей на русском
const RARITY_NAMES = {
    consumer:   "Ширпотреб",
    industrial: "Промышленное",
    milspec:    "Армейское",
    restricted: "Запрещённое",
    classified: "Засекреченное",
    covert:     "Тайное",
    contraband: "Контрабанда"
};

// ===================== УТИЛИТЫ =====================

function $(id){ return document.getElementById(id); }

function toast(msg, type="t-green"){
    const t = $("toast");
    t.textContent = msg;
    t.className = "toast show " + type;
    setTimeout(()=>{ t.className = "toast"; }, 3200);
}

function saveData(){
    localStorage.setItem("cscase_users", JSON.stringify(users));
    if(currentUser){
        localStorage.setItem("cscase_current", currentUser);
    }
}

function loadData(){
    const u = localStorage.getItem("cscase_users");
    if(u) users = JSON.parse(u);
    const c = localStorage.getItem("cscase_current");
    if(c) currentUser = c;
}

function getUser(name){
    return users.find(u => u.name === name);
}

function updateBalanceUI(){
    const u = getUser(currentUser);
    if(!u) return;
    $("bal-num").textContent = u.balance;
    $("welcome-name").textContent = "Привет, " + u.name + "! 👋";
    $("username-badge").textContent = u.name;
    updateInvStats();
}

function updateInvStats(){
    const u = getUser(currentUser);
    if(!u) return;
    $("stat-count").textContent = u.inventory.length;
    const total = u.inventory.reduce((s,i)=>s+i.value,0);
    $("stat-total").textContent = total + " ₽";
    $("stat-withdrawn").textContent = (u.withdrawn||0) + "/10";
}

// ===================== АВТОРИЗАЦИЯ =====================

let users = [];
let currentUser = null;

function switchAuthTab(tab){
    document.querySelectorAll(".auth-tab").forEach(b=>b.classList.remove("active"));
    document.querySelectorAll(".auth-form").forEach(f=>f.classList.remove("active"));
    event.target.classList.add("active");
    $("form-"+tab).classList.add("active");
    $("auth-err").style.display = "none";
}

function showErr(msg){
    const e = $("auth-err");
    e.textContent = msg;
    e.style.display = "block";
}

function doLogin(){
    const name = $("inp-login").value.trim();
    const pass = $("inp-pass").value;
    if(!name || !pass){ showErr("Заполни все поля"); return; }
    const u = getUser(name);
    if(!u){ showErr("Такого пользователя нет"); return; }
    if(u.password !== pass){ showErr("Неверный пароль"); return; }
    currentUser = name;
    saveData();
    enterSite();
}

function doRegister(){
    const name = $("inp-reg-login").value.trim();
    const pass = $("inp-reg-pass").value;
    const pass2 = $("inp-reg-pass2").value;
    if(!name || !pass || !pass2){ showErr("Заполни все поля"); return; }
    if(name.length < 3){ showErr("Логин минимум 3 символа"); return; }
    if(pass.length < 4){ showErr("Пароль минимум 4 символа"); return; }
    if(pass !== pass2){ showErr("Пароли не совпадают"); return; }
    if(getUser(name)){ showErr("Такой логин уже занят"); return; }
    const newUser = {
        name: name,
        password: pass,
        balance: 150,
        inventory: [],
        withdrawn: 0
    };
    users.push(newUser);
    currentUser = name;
    saveData();
    enterSite();
    toast("🎉 Регистрация прошла! Тебе начислено 150 ₽", "t-orange");
}

function enterSite(){
    $("page-auth").classList.remove("active");
    $("page-main").classList.add("active");
    $("main-nav").style.display = "flex";
    $("balance-badge").style.display = "block";
    $("username-badge").style.display = "block";
    $("btn-logout").style.display = "block";
    updateBalanceUI();
    renderCases();
    renderInventory();
}

function logout(){
    currentUser = null;
    localStorage.removeItem("cscase_current");
    $("page-main").classList.remove("active");
    $("page-auth").classList.add("active");
    $("main-nav").style.display = "none";
    $("balance-badge").style.display = "none";
    $("username-badge").style.display = "none";
    $("btn-logout").style.display = "none";
    $("inp-login").value = "";
    $("inp-pass").value = "";
}

// ===================== ВКЛАДКИ =====================

function showTab(tab){
    document.querySelectorAll(".tab-btn").forEach(b=>b.classList.remove("active"));
    $("tab-"+tab).classList.add("active");
    $("section-cases").style.display = tab==="cases" ? "block" : "none";
    $("section-inventory").style.display = tab==="inventory" ? "block" : "none";
    if(tab === "inventory") renderInventory();
}

// ===================== РЕНДЕР КЕЙСОВ =====================

function renderCases(){
    const grid = $("cases-grid");
    grid.innerHTML = "";
    CASES.forEach(c=>{
        const card = document.createElement("div");
        card.className = "case-card";
        card.innerHTML = `
            <div class="case-img" style="background:${c.bg}">
                <span>${c.emoji}</span>
                <div class="case-badge">${c.price} ₽</div>
            </div>
            <div class="case-info">
                <div class="case-name">${c.name}</div>
                <div class="case-price-row">
                    <span class="case-price">${c.price} ₽</span>
                    <button class="case-open-btn">Открыть</button>
                </div>
            </div>
        `;
        card.onclick = () => openModal(c.id);
        grid.appendChild(card);
    });
}

// ===================== МОДАЛКА + РУЛЕТКА =====================

let currentCaseId = null;
let wonSkin = null;
let isSpinning = false;

function openModal(caseId){
    currentCaseId = caseId;
    wonSkin = null;
    isSpinning = false;
    const c = CASES.find(x=>x.id===caseId);
    const u = getUser(currentUser);

    $("m-case-name").textContent = c.name;
    $("m-case-sub").textContent = "Цена открытия: " + c.price + " ₽";
    $("result-wrap").classList.remove("show");
    $("btn-sell-win").classList.remove("show");
    $("btn-keep-win").classList.remove("show");
    $("no-bal-msg").classList.remove("show");
    $("btn-do-open").disabled = false;
    $("btn-do-open").style.display = "block";

    if(u.balance < c.price){
        $("no-bal-msg").classList.add("show");
        $("btn-do-open").disabled = true;
    }

    buildRoulette(c);
    $("case-overlay").classList.add("show");
}

function buildRoulette(c){
    const track = $("r-track");
    track.style.transition = "none";
    track.style.transform = "translateX(0)";
    track.innerHTML = "";

    // Генерим 60 случайных скинов для рулетки
    const items = [];
    for(let i=0;i<60;i++){
        items.push(c.skins[Math.floor(Math.random()*c.skins.length)]);
    }

    items.forEach(skin=>{
        const el = document.createElement("div");
        el.className = `r-item rarity-${skin.rarity}`;
        el.innerHTML = `
            <div class="r-item-icon">${skin.emoji}</div>
            <div class="r-item-name">${skin.name}</div>
        `;
        track.appendChild(el);
    });
}

function rollSkin(c){
    // Взвешенный рандом
    const total = c.skins.reduce((s,x)=>s+x.chance,0);
    let r = Math.random()*total;
    for(const skin of c.skins){
        r -= skin.chance;
        if(r <= 0) return skin;
    }
    return c.skins[0];
}

function openCase(){
    if(isSpinning) return;
    const c = CASES.find(x=>x.id===currentCaseId);
    const u = getUser(currentUser);
    if(u.balance < c.price){
        $("no-bal-msg").classList.add("show");
        return;
    }

    // Списываем баланс
    u.balance -= c.price;
    saveData();
    updateBalanceUI();

    isSpinning = true;
    $("btn-do-open").disabled = true;
    $("result-wrap").classList.remove("show");
    $("btn-sell-win").classList.remove("show");
    $("btn-keep-win").classList.remove("show");

    wonSkin = rollSkin(c);

    const track = $("r-track");
    const items = track.querySelectorAll(".r-item");

    // Ставим выигрышный скин на позицию 45
    const winIndex = 45;
    const winEl = items[winIndex];
    winEl.innerHTML = `
        <div class="r-item-icon">${wonSkin.emoji}</div>
        <div class="r-item-name">${wonSkin.name}</div>
    `;
    winEl.className = `r-item rarity-${wonSkin.rarity}`;

    // Считаем смещение — центр winIndex под линию
    const itemW = 118; // 112 + 6 gap
    const containerW = document.querySelector(".roulette-outer").offsetWidth;
    const offset = winIndex * itemW - (containerW/2 - 56) + (Math.random()*60 - 30);

    setTimeout(()=>{
        track.style.transition = "transform 4.5s cubic-bezier(.17,.67,.08,1)";
        track.style.transform = `translateX(-${offset}px)`;
    }, 50);

    setTimeout(()=>{
        showResult();
        isSpinning = false;
    }, 4700);
}

function showResult(){
    const card = $("result-card");
    card.className = `result-card-big rarity-${wonSkin.rarity}`;
    $("res-icon").textContent = wonSkin.emoji;
    $("res-name").textContent = wonSkin.name;
    $("res-rarity").textContent = RARITY_NAMES[wonSkin.rarity] || wonSkin.rarity;
    $("res-rarity").className = `result-rarity-label rl-${wonSkin.rarity}`;
    $("res-val").textContent = wonSkin.value + " ₽";
    $("result-wrap").classList.add("show");
    $("btn-sell-win").classList.add("show");
    $("btn-keep-win").classList.add("show");
    $("btn-do-open").style.display = "none";
}

function sellWon(){
    if(!wonSkin) return;
    const u = getUser(currentUser);
    u.balance += wonSkin.value;
    saveData();
    updateBalanceUI();
    toast(`💰 Продал ${wonSkin.name} за ${wonSkin.value} ₽`, "t-green");
    wonSkin = null;
    closeModal();
}

function keepWon(){
    if(!wonSkin) return;
    const u = getUser(currentUser);
    const invSkin = Object.assign({ id: Date.now() + Math.random() }, wonSkin);
    u.inventory.push(invSkin);
    saveData();
    updateBalanceUI();
    toast(`🎒 ${wonSkin.name} добавлен в инвентарь!`, "t-orange");
    wonSkin = null;
    closeModal();
}

function closeModal(){
    $("case-overlay").classList.remove("show");
    wonSkin = null;
    isSpinning = false;
}

// Клик вне модалки — закрываем
$("case-overlay").addEventListener("click", function(e){
    if(e.target === this && !isSpinning) closeModal();
});

// ===================== ИНВЕНТАРЬ =====================

function renderInventory(){
    const u = getUser(currentUser);
    if(!u) return;
    const grid = $("inv-grid");
    grid.innerHTML = "";
    updateInvStats();

    if(u.inventory.length === 0){
        grid.innerHTML = `
            <div class="inv-empty">
                <div>🎒</div>
                <div>Инвентарь пустой</div>
                <div style="font-size:13px;margin-top:8px">Открывай кейсы и собирай скины</div>
            </div>
        `;
        return;
    }

    u.inventory.forEach(skin=>{
        const canWithdraw = (u.withdrawn||0) < 10;
        const card = document.createElement("div");
        card.className = "inv-card";
        card.innerHTML = `
            <div class="inv-card-img rarity-${skin.rarity}" style="background:unset">
                <span style="font-size:38px">${skin.emoji}</span>
            </div>
            <div class="inv-card-info">
                <div class="inv-card-name">${skin.name}</div>
                <div class="inv-card-rarity rl-${skin.rarity}">${RARITY_NAMES[skin.rarity]||skin.rarity}</div>
                <div class="inv-card-val">${skin.value} ₽</div>
                <div class="inv-card-btns">
                    <button class="btn-inv-sell" onclick="sellInvSkin('${skin.id}')">💰 Продать</button>
                    <button class="btn-inv-withdraw" onclick="withdrawSkin('${skin.id}')" ${canWithdraw?"":'disabled title="Лимит вывода 10 штук"'}>
                        📤 Вывод
                    </button>
                </div>
            </div>
        `;
        grid.appendChild(card);
    });
}

function sellInvSkin(skinId){
    const u = getUser(currentUser);
    const idx = u.inventory.findIndex(s=>String(s.id)===String(skinId));
    if(idx === -1) return;
    const skin = u.inventory[idx];
    u.balance += skin.value;
    u.inventory.splice(idx, 1);
    saveData();
    updateBalanceUI();
    renderInventory();
    toast(`💰 Продал ${skin.name} за ${skin.value} ₽`, "t-green");
}

function withdrawSkin(skinId){
    const u = getUser(currentUser);
    if((u.withdrawn||0) >= 10){
        toast("❌ Лимит вывода исчерпан (10/10)", "t-red");
        return;
    }
    const idx = u.inventory.findIndex(s=>String(s.id)===String(skinId));
    if(idx === -1) return;
    const skin = u.inventory[idx];
    u.inventory.splice(idx, 1);
    u.withdrawn = (u.withdrawn||0) + 1;
    saveData();
    updateBalanceUI();
    renderInventory();
    toast(`📤 ${skin.name} выведен! (${u.withdrawn}/10)`, "t-blue");
}

// ===================== ИНИЦИАЛИЗАЦИЯ =====================

loadData();

if(currentUser && getUser(currentUser)){
    enterSite();
}

</script>
</body>
</html>


---

Это **часть 1** — вся разметка и стили готовы. Пишу **часть 2** — данные кейсов и JS логику?
