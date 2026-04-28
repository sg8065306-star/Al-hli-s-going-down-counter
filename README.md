<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
    <title>⏳ عداد هبوط الأهلي | دوري يلو</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
            touch-action: manipulation;
        }

        html {
            height: 100%;
            background: #010a08;
        }

        body {
            margin: 0;
            min-height: 100vh;
            min-height: 100dvh;
            /* تعديل المساحة العلوية لتتناسب مع البار الأصغر */
            padding-top: calc(24vh + env(safe-area-inset-top) + 8px);
            padding-left: env(safe-area-inset-left);
            padding-right: env(safe-area-inset-right);
            background: radial-gradient(ellipse at 30% 40%, #0a2f2a, #010a08);
            font-family: 'Segoe UI', 'Tahoma', 'Cairo', system-ui, -apple-system, BlinkMacSystemFont, sans-serif;
            display: flex;
            align-items: flex-start;
            justify-content: center;
            overflow-x: hidden;
            -webkit-text-size-adjust: 100%;
            position: relative;
        }

        .top-bar {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: auto;
            /* تقليص الحجم بنسبة 10%: 30.3vh >> 27.3vh */
            min-height: 27.3vh;
            background: url('https://i.ibb.co/XfY4TcH7/EC3-DE5-E1-58-D1-4-F19-831-D-28142868695-A.png') no-repeat center center;
            background-size: cover;
            border-bottom: 2px solid rgba(0, 255, 200, 0.35);
            box-shadow: 0 6px 14px rgba(0, 0, 0, 0.5);
            display: flex;
            align-items: flex-end;
            justify-content: center;
            z-index: 9999;
            padding-bottom: 8px; /* تقليل بسيط إضافي */
            padding-top: env(safe-area-inset-top);
            box-sizing: border-box;
            pointer-events: none;
        }
        
        .top-bar .highlight-box {
            pointer-events: auto;
            background: rgba(0, 15, 12, 0.8);
            backdrop-filter: blur(12px);
            border-radius: 50px;
            padding: 8px 18px;
            margin-bottom: 10px;
            border: 1px solid rgba(0, 255, 200, 0.7);
            box-shadow: 0 0 14px rgba(0, 255, 200, 0.4), inset 0 0 6px rgba(0, 255, 200, 0.2);
        }
        
        .top-bar .highlight-box span {
            font-weight: bold;
            color: #eafff0;
            font-size: clamp(0.68rem, 3.52vw, 0.88rem);
            text-align: center;
            text-shadow: 0 0 5px #00ccaa;
            letter-spacing: 0.3px;
            line-height: 1.45;
        }

        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: repeating-linear-gradient(45deg, rgba(0,255,200,0.02) 0px, rgba(0,255,200,0.02) 2px, transparent 2px, transparent 8px);
            pointer-events: none;
            z-index: 0;
        }

        .card {
            position: relative;
            z-index: 2;
            background: rgba(5, 25, 22, 0.72);
            backdrop-filter: blur(18px);
            border-radius: 48px;
            padding: 22px 20px 28px;
            max-width: 600px;
            width: 100%;
            margin: 0px 16px 24px 16px;
            text-align: center;
            box-shadow: 0 35px 55px rgba(0, 0, 0, 0.6), 0 0 0 1.5px rgba(0, 255, 200, 0.3), 0 0 20px rgba(0, 255, 200, 0.3);
            border: 1px solid rgba(0, 255, 200, 0.4);
        }

        .counter-box {
            position: relative;
            margin: 12px 0 16px;
            overflow: visible;
            border-radius: 40px;
            background: transparent;
            box-shadow: none;
        }

        .clock-wrapper {
            position: relative;
            width: 90%;
            max-width: 320px;
            margin: auto;
        }

        .clock-image {
            display: block;
            width: 100%;
            height: auto;
            border-radius: 20px;
            pointer-events: none;
        }

        .clock-hands {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 20;
        }

        .hand {
            position: absolute;
            bottom: 50%;
            left: 50%;
            transform-origin: 50% 100%;
            border-radius: 30% 30% 10% 10% / 60% 60% 20% 20%;
            box-shadow: 0 0 4px rgba(0,0,0,0.3), 0 1px 2px rgba(0,0,0,0.2);
        }

        .hour-hand {
            width: 6px;
            height: 24%;
            background: linear-gradient(135deg, #e6c27a, #b48c3a, #8a6125);
            border-radius: 8px 8px 4px 4px;
            filter: drop-shadow(0 0 2px rgba(0,0,0,0.5));
        }
        
        .minute-hand {
            width: 4.5px;
            height: 34%;
            background: linear-gradient(135deg, #f0d48e, #c9a045, #9e752e);
            border-radius: 6px 6px 3px 3px;
            filter: drop-shadow(0 0 2px rgba(0,0,0,0.4));
        }
        
        .second-hand {
            width: 2.2px;
            height: 40%;
            background: linear-gradient(0deg, #f5c542, #d4a52a, #f0c060);
            border-radius: 2px 2px 1px 1px;
            box-shadow: 0 0 6px rgba(212, 165, 42, 0.6);
            transition: none !important;
        }
        
        .center-dot {
            position: absolute;
            top: 50%;
            left: 50%;
            width: 10px;
            height: 10px;
            background: radial-gradient(circle, #f5e2b0, #c9a045);
            border-radius: 50%;
            transform: translate(-50%, -50%);
            box-shadow: 0 0 6px #d4af37;
            z-index: 25;
            border: 1px solid #fff3cf;
        }

        .counter, .units {
            display: none;
        }

        .counter-digit {
            position: absolute;
            color: #00ffc3;
            font-weight: bold;
            font-size: clamp(1.05rem, 3.75vw, 1.5rem);
            text-shadow: 0 0 8px #00ffc3, 0 0 3px #00aa88;
            font-family: 'Fira Mono', 'Courier New', monospace;
            background: rgba(0,0,0,0.45);
            backdrop-filter: blur(4px);
            padding: 2px 6px;
            border-radius: 24px;
            white-space: nowrap;
            direction: ltr;
            letter-spacing: 0.5px;
            top: 72%;
            transform: translate(-50%, -50%);
            z-index: 15;
        }

        .days { left: 22%; }
        .hours { left: 41.5%; }
        .minutes { left: 58.5%; }
        .seconds { left: 77%; }

        /* مربعات السنوات والشهور */
        .stats-row {
            display: flex;
            justify-content: center;
            gap: 16px;
            margin: 16px 0 8px;
            flex-wrap: wrap;
        }
        .stat-card {
            background: rgba(0, 20, 18, 0.75);
            backdrop-filter: blur(8px);
            border-radius: 32px;
            padding: 8px 18px;
            min-width: 110px;
            text-align: center;
            border: 1px solid rgba(0, 255, 200, 0.5);
            box-shadow: 0 0 12px rgba(0, 255, 200, 0.2);
        }
        .stat-number {
            font-size: clamp(1.6rem, 6vw, 2.4rem);
            font-weight: bold;
            color: #ffecb3;
            text-shadow: 0 0 6px #ffcc77;
            line-height: 1.2;
            font-family: 'Fira Mono', monospace;
            direction: ltr;
        }
        .stat-label {
            font-size: 0.7rem;
            color: #aaffee;
            letter-spacing: 1px;
            margin-top: 4px;
            text-transform: uppercase;
        }

        .contact-area {
            margin-top: 20px;
            background: rgba(0, 30, 26, 0.7);
            backdrop-filter: blur(8px);
            border-radius: 60px;
            padding: 12px 16px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
            flex-wrap: wrap;
            border: 0.5px solid rgba(0, 255, 200, 0.4);
        }
        .contact-text {
            font-size: 0.85rem;
            color: #effffa;
            font-weight: 500;
        }
        .whatsapp-icon {
            width: 24px;
            height: 24px;
            filter: drop-shadow(0 0 3px #25D366);
        }
        .whatsapp-link {
            display: inline-flex;
            align-items: center;
            gap: 6px;
            text-decoration: none;
            background: #075e5440;
            padding: 6px 14px;
            border-radius: 40px;
            transition: all 0.2s;
            border: 0.5px solid #6effdc60;
        }
        .whatsapp-link:active {
            transform: scale(0.97);
            background: #25d36640;
        }
        .whatsapp-link span {
            color: #dafef2;
            font-weight: 600;
            font-size: 0.85rem;
            direction: ltr;
        }

        /* تحسينات للأجهزة المحمولة (كما كانت) */
        @media (max-width: 550px) {
            body { padding-top: calc(15vh + env(safe-area-inset-top) + 5px); } /* تقليل طفيف مع البار الأصغر */
            .card { padding: 18px 14px 24px; border-radius: 40px; margin: 0 12px 20px 12px; }
            .counter-digit { font-size: clamp(0.9rem, 3.2vw, 1.2rem); padding: 1px 4px; }
            .hour-hand { width: 5px; height: 22%; }
            .minute-hand { width: 3.5px; height: 30%; }
            .second-hand { width: 1.8px; height: 37%; }
            .center-dot { width: 8px; height: 8px; }
            .stat-card { min-width: 85px; padding: 6px 12px; }
            .stat-number { font-size: 1.8rem; }
        }

        @media (max-width: 400px) {
            .counter-digit { font-size: clamp(0.8rem, 2.8vw, 1rem); padding: 1px 3px; }
        }

        /* دعم شاشات الكمبيوتر المكتبي */
        @media (min-width: 1024px) {
            body {
                padding-top: calc(22vh + env(safe-area-inset-top) + 8px);
                align-items: center; /* توسيط عمودي أفضل على الشاشات الكبيرة */
            }
            .card {
                max-width: 720px;
                margin: 0 auto 30px;
                padding: 30px 28px 35px;
            }
            .top-bar .highlight-box span {
                font-size: 1rem;
            }
            .clock-wrapper {
                max-width: 380px;
            }
            .counter-digit {
                font-size: clamp(1.2rem, 2vw, 1.7rem);
                padding: 4px 10px;
                top: 70%;
            }
            .stat-card {
                min-width: 130px;
                padding: 12px 22px;
            }
            .stat-number {
                font-size: 2.6rem;
            }
            .stat-label {
                font-size: 0.85rem;
            }
            .contact-area {
                padding: 14px 24px;
                gap: 18px;
            }
        }

        /* لشاشات أكبر (عريضة) */
        @media (min-width: 1440px) {
            .card {
                max-width: 850px;
            }
            .clock-wrapper {
                max-width: 440px;
            }
        }
    </style>
</head>
<body>

<div class="top-bar">
    <div class="highlight-box">
        <span>📉 عداد هبوط نادي الأهلي إلى دوري يلو منذ ٢٧ يونيو ٢٠٢٢</span>
    </div>
</div>

<div class="card">
    <!-- تم حذف صورة شعار الأهلي بناءً على الطلب السابق -->
    
    <div class="counter-box">
        <div class="clock-wrapper">
            <img class="clock-image" src="https://i.ibb.co/39JVpBJ2/38-AD4942-B88-A-4757-A02-E-CEE99-DF39245.png" alt="خلفية الساعة">
            <div class="clock-hands">
                <div class="hand hour-hand" id="hour-hand"></div>
                <div class="hand minute-hand" id="minute-hand"></div>
                <div class="hand second-hand" id="second-hand"></div>
                <div class="center-dot"></div>
            </div>
            <div class="counter-digit days" id="daysDigit">0</div>
            <div class="counter-digit hours" id="hoursDigit">00</div>
            <div class="counter-digit minutes" id="minutesDigit">00</div>
            <div class="counter-digit seconds" id="secondsDigit">00</div>
        </div>
    </div>
    
    <!-- مربعات السنوات والشهور -->
    <div class="stats-row">
        <div class="stat-card">
            <div class="stat-number" id="yearsValue">0</div>
            <div class="stat-label">سنوات</div>
        </div>
        <div class="stat-card">
            <div class="stat-number" id="monthsValue">0</div>
            <div class="stat-label">أشهر</div>
        </div>
    </div>
    
    <div class="contact-area">
        <span class="contact-text">📞 للاستفسار والتواصل:</span>
        <strong style="color:#eafff0;">أحمد العتيبي</strong>
        <a href="https://wa.me/966551162550" target="_blank" class="whatsapp-link" rel="noopener noreferrer">
            <img class="whatsapp-icon" src="https://upload.wikimedia.org/wikipedia/commons/6/6b/WhatsApp.svg" alt="WhatsApp">
            <span>055 116 2550</span>
        </a>
    </div>
    <!-- تم حذف الفوتر بالكامل بناءً على الطلب -->
</div>

<script>
    (function() {
        const hourHand = document.getElementById('hour-hand');
        const minuteHand = document.getElementById('minute-hand');
        const secondHand = document.getElementById('second-hand');
        
        const daysEl = document.getElementById('daysDigit');
        const hoursEl = document.getElementById('hoursDigit');
        const minutesEl = document.getElementById('minutesDigit');
        const secondsEl = document.getElementById('secondsDigit');
        
        const yearsEl = document.getElementById('yearsValue');
        const monthsEl = document.getElementById('monthsValue');
        
        const relegationDate = new Date("2022-06-27T00:00:00+03:00");
        
        let lastSyncedRiyadhTime = null;
        let lastSyncPerf = null;
        let hasValidSync = false;
        
        function getCurrentRiyadhTime() {
            if (hasValidSync && lastSyncedRiyadhTime && lastSyncPerf !== null) {
                const elapsedMs = performance.now() - lastSyncPerf;
                return new Date(lastSyncedRiyadhTime.getTime() + elapsedMs);
            }
            const nowDevice = new Date();
            return new Date(nowDevice.getTime() + (3 * 60 * 60 * 1000));
        }
        
        function computeTimeDifference(riyadhNow) {
            if (!riyadhNow || isNaN(riyadhNow.getTime())) return null;
            let diffMs = riyadhNow - relegationDate;
            if (diffMs < 0) diffMs = 0;
            const totalSeconds = Math.floor(diffMs / 1000);
            const days = Math.floor(totalSeconds / 86400);
            const hours = Math.floor((totalSeconds % 86400) / 3600);
            const minutes = Math.floor((totalSeconds % 3600) / 60);
            const seconds = totalSeconds % 60;
            return { days, hours, minutes, seconds };
        }
        
        function getYearsMonthsSince(relegation, current) {
            let years = current.getFullYear() - relegation.getFullYear();
            let months = current.getMonth() - relegation.getMonth();
            if (months < 0) {
                years--;
                months += 12;
            }
            if (current.getDate() < relegation.getDate()) {
                months--;
                if (months < 0) {
                    years--;
                    months += 12;
                }
            }
            return { years: Math.max(0, years), months: Math.max(0, months) };
        }
        
        function updateCounter(diff) {
            if (!diff) {
                daysEl.textContent = '0';
                hoursEl.textContent = '00';
                minutesEl.textContent = '00';
                secondsEl.textContent = '00';
                return;
            }
            daysEl.textContent = diff.days.toString();
            hoursEl.textContent = diff.hours < 10 ? '0' + diff.hours : diff.hours.toString();
            minutesEl.textContent = diff.minutes < 10 ? '0' + diff.minutes : diff.minutes.toString();
            secondsEl.textContent = diff.seconds < 10 ? '0' + diff.seconds : diff.seconds.toString();
        }
        
        function updateYearsMonths(riyadhNow) {
            if (!riyadhNow) return;
            const { years, months } = getYearsMonthsSince(relegationDate, riyadhNow);
            yearsEl.textContent = years;
            monthsEl.textContent = months;
        }
        
        function updateClockHands(riyadhTime) {
            if (!riyadhTime) return;
            const adjustedTime = new Date(riyadhTime.getTime() + (16 * 60 * 1000));
            let hours = adjustedTime.getHours() % 12;
            let minutes = adjustedTime.getMinutes();
            let seconds = riyadhTime.getSeconds() + riyadhTime.getMilliseconds() / 1000;
            
            const secondDeg = seconds * 6 - 90;
            const minuteDeg = minutes * 6 + seconds * 0.1 - 90;
            const hourDeg = (hours * 30) + (minutes * 0.5) - 90;
            
            secondHand.style.transform = `translateX(-50%) rotate(${secondDeg}deg)`;
            minuteHand.style.transform = `translateX(-50%) rotate(${minuteDeg}deg)`;
            hourHand.style.transform = `translateX(-50%) rotate(${hourDeg}deg)`;
        }
        
        function updateAll() {
            const now = getCurrentRiyadhTime();
            const diff = computeTimeDifference(now);
            updateCounter(diff);
            updateYearsMonths(now);
            updateClockHands(now);
        }
        
        async function syncWithAPI() {
            try {
                const controller = new AbortController();
                const timeoutId = setTimeout(() => controller.abort(), 6000);
                const response = await fetch("https://worldtimeapi.org/api/timezone/Asia/Riyadh", {
                    signal: controller.signal,
                    cache: "no-store"
                });
                clearTimeout(timeoutId);
                if (!response.ok) throw new Error(`HTTP ${response.status}`);
                const data = await response.json();
                if (!data || !data.utc_datetime) throw new Error("Invalid response");
                const utcDate = new Date(data.utc_datetime);
                if (isNaN(utcDate.getTime())) throw new Error("Invalid UTC date");
                const riyadhTime = new Date(utcDate.getTime() + (3 * 60 * 60 * 1000));
                lastSyncedRiyadhTime = riyadhTime;
                lastSyncPerf = performance.now();
                hasValidSync = true;
                updateAll();
            } catch (err) {
                updateAll();
            }
        }
        
        let intervalId = null;
        let resyncId = null;
        
        function startIntervals() {
            if (intervalId) clearInterval(intervalId);
            intervalId = setInterval(() => updateAll(), 1000);
            if (resyncId) clearInterval(resyncId);
            resyncId = setInterval(() => syncWithAPI(), 30000);
        }
        
        startIntervals();
        syncWithAPI();
        
        document.addEventListener("visibilitychange", () => {
            if (!document.hidden) {
                updateAll();
                if (!hasValidSync) syncWithAPI();
            }
        });
    })();
</script>
</body>
</html>
