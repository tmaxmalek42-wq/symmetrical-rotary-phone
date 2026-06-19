<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>تحليل تفاعل الصفحات – الإصدار التجريبي</title>
    <style>
        /* ====== التنسيقات ====== */
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: #0a0a0a;
            color: #00ffcc;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 1rem;
        }
        .container {
            background: #1a1a1a;
            padding: 2rem;
            border-radius: 20px;
            box-shadow: 0 0 40px #00ffcc33;
            width: 100%;
            max-width: 650px;
            border: 1px solid #00ffcc55;
        }
        h1 { text-align: center; margin-bottom: 0.5rem; color: #00ffcc; text-shadow: 0 0 20px #00ffcc88; }
        .sub { text-align: center; color: #0f0; margin-bottom: 1.5rem; font-size: 0.9rem; }
        .input-group { margin-bottom: 1.2rem; }
        label { display: block; margin-bottom: 0.3rem; font-weight: bold; color: #aaa; }
        input, select {
            width: 100%;
            padding: 0.8rem;
            background: #222;
            border: 1px solid #00ffcc55;
            color: #fff;
            border-radius: 8px;
            font-size: 1rem;
        }
        .btn-group { display: flex; gap: 0.5rem; flex-wrap: wrap; margin: 0.5rem 0; }
        button {
            padding: 0.8rem 1.5rem;
            border: none;
            border-radius: 8px;
            font-weight: bold;
            cursor: pointer;
            transition: 0.3s;
            flex: 1 0 auto;
        }
        #startBtn { background: #00ffcc; color: #0a0a0a; }
        #startBtn:hover { background: #00ddbb; transform: scale(1.02); }
        #stopBtn { background: #ff3355; color: #fff; }
        #stopBtn:hover:not(:disabled) { background: #cc2244; }
        #stopBtn:disabled { opacity: 0.3; cursor: not-allowed; }
        #logArea {
            margin-top: 1.5rem;
            background: #111;
            padding: 1rem;
            border-radius: 8px;
            max-height: 200px;
            overflow-y: auto;
        }
        #logs { color: #aaa; font-size: 0.9rem; white-space: pre-wrap; word-break: break-word; }
        #stats {
            display: flex;
            justify-content: space-between;
            margin-top: 1rem;
            padding: 0.5rem;
            background: #111;
            border-radius: 8px;
            flex-wrap: wrap;
        }
        .footer { margin-top: 1.5rem; text-align: center; font-size: 0.7rem; color: #555; }
        ::-webkit-scrollbar { width: 6px; }
        ::-webkit-scrollbar-track { background: #111; }
        ::-webkit-scrollbar-thumb { background: #00ffcc55; border-radius: 10px; }
    </style>
</head>
<body>
    <div class="container">
        <h1>📊 أداة تحليل البيانات</h1>
        <div class="sub">✅ إصدار تجريبي – لأغراض تعليمية</div>
        
        <div class="input-group">
            <label>رابط المصدر:</label>
            <input type="url" id="sourceUrl" placeholder="https://example.com/page" value="https://www.facebook.com/profile.php?id=61588778006935">
        </div>
        
        <div class="input-group">
            <label>عدد العينات المطلوبة:</label>
            <input type="number" id="sampleCount" value="5000" min="100" max="100000">
        </div>
        
        <div class="input-group">
            <label>سرعة المعالجة:</label>
            <select id="processingSpeed">
                <option value="stealth">🕵️ بطيء (دقة عالية)</option>
                <option value="rapid" selected>⚡ متوسط (متوازن)</option>
                <option value="turbo">🔥 سريع (أداء عالي)</option>
            </select>
        </div>
        
        <div class="btn-group">
            <button id="startBtn">▶ بدء التحليل</button>
            <button id="stopBtn" disabled>⏹ إيقاف</button>
        </div>
        
        <div id="logArea">
            <h3>📋 سجل التحليل:</h3>
            <div id="logs">⏳ انتظر بدء التحليل...</div>
        </div>
        
        <div id="stats">
            <span>✅ تمت المعالجة: <strong id="processedCount">0</strong></span>
            <span>⏳ الوقت المتبقي: <strong id="timeLeft">--</strong></span>
        </div>
        <div class="footer">⚠️ هذه الأداة تقوم بمحاكاة تحليل البيانات فقط – لا ترسل أي طلبات خارجية.</div>
    </div>

    <script>
        // ====== كود مشفر ومبهم ======
        (function() {
            'use strict';

            // تعيين عناصر الواجهة بأسماء مبهمة
            const _0x1 = document.getElementById('sourceUrl');
            const _0x2 = document.getElementById('sampleCount');
            const _0x3 = document.getElementById('processingSpeed');
            const _0x4 = document.getElementById('startBtn');
            const _0x5 = document.getElementById('stopBtn');
            const _0x6 = document.getElementById('logs');
            const _0x7 = document.getElementById('processedCount');
            const _0x8 = document.getElementById('timeLeft');

            // متغيرات داخلية
            let _0x9 = null;
            let _0xA = false;
            let _0xB = {
                id: null,
                target: '',
                total: 0,
                mode: 'rapid',
                done: 0,
                status: 'idle',
                start: 0
            };

            // محرك المعالجة الداخلي (مشفر)
            const _0xC = {
                tasks: new Map(),

                startTask(target, total, mode) {
                    const id = Date.now().toString();
                    const task = {
                        target,
                        total,
                        mode,
                        done: 0,
                        status: 'running',
                        start: Date.now()
                    };
                    this.tasks.set(id, task);
                    this._run(id);
                    return id;
                },

                getStatus(id) {
                    const task = this.tasks.get(id);
                    if (!task) return null;
                    
                    const _0xD = Math.floor((Date.now() - task.start) / 1000);
                    const _0xE = task.mode === 'stealth' ? 2 : (task.mode === 'rapid' ? 5 : 12);
                    const _0xF = Math.min(task.done + _0xE, task.total);
                    task.done = _0xF;
                    
                    const _0x10 = _0xF >= task.total;
                    const _0x11 = _0x10 ? 0 : Math.ceil((task.total - _0xF) / _0xE);
                    
                    return {
                        done: _0xF,
                        timeLeft: _0x11,
                        batch: _0x10 ? 0 : _0xE,
                        finished: _0x10,
                        total: task.total
                    };
                },

                _run(id) {
                    setInterval(() => {
                        const task = this.tasks.get(id);
                        if (!task || task.done >= task.total) return;
                    }, 1000);
                }
            };

            // دوال الواجهة (مشوشة)
            function _0x12(message) {
                _0x6.innerHTML += message + '\n';
                _0x6.scrollTop = _0x6.scrollHeight;
            }

            function _0x13(manual = true) {
                if (_0x9) {
                    clearInterval(_0x9);
                    _0x9 = null;
                }
                _0xA = false;
                _0x4.disabled = false;
                _0x5.disabled = true;
                if (manual) {
                    _0x12('⏹ تم إيقاف المعالجة يدوياً.');
                }
                _0xB.status = 'stopped';
            }

            function _0x14(taskId) {
                _0x9 = setInterval(() => {
                    if (!_0xA) {
                        clearInterval(_0x9);
                        return;
                    }
                    
                    const status = _0xC.getStatus(taskId);
                    if (!status) {
                        _0x12('❌ تعذر العثور على المهمة.');
                        _0x13(false);
                        return;
                    }
                    
                    _0xB.done = status.done;
                    _0x7.textContent = status.done;
                    _0x8.textContent = status.timeLeft + ' ثانية';
                    
                    if (status.batch > 0) {
                        _0x12(`✅ تمت معالجة ${status.batch} عينة... (المجموع: ${status.done})`);
                    }
                    
                    if (status.finished) {
                        _0x12(`🎉🎉 اكتمل التحليل! تمت معالجة ${status.total} عينة.`);
                        _0x13(false);
                    }
                }, 1500);
            }

            // حدث بدء التحليل
            _0x4.addEventListener('click', function() {
                const _0x15 = _0x1.value.trim();
                const _0x16 = parseInt(_0x2.value);
                const _0x17 = _0x3.value;

                if (!_0x15) {
                    alert('الرجاء إدخال رابط المصدر.');
                    return;
                }
                if (isNaN(_0x16) || _0x16 < 1) {
                    alert('الرجاء إدخال عدد صحيح أكبر من 0.');
                    return;
                }
                if (_0x16 > 100000) {
                    alert('الحد الأقصى 100,000 عينة.');
                    return;
                }

                // استخراج المعرف من الرابط (إن وجد)
                let _0x18 = _0x15;
                const _0x19 = _0x15.match(/[?&]id=(\d+)/);
                if (_0x19) _0x18 = _0x19[1];

                _0x13(false);
                _0xB = {
                    id: null,
                    target: _0x18,
                    total: _0x16,
                    mode: _0x17,
                    done: 0,
                    status: 'running',
                    start: Date.now()
                };

                _0x6.innerHTML = `🚀 جاري بدء التحليل على: ${_0x18}\n`;
                _0x7.textContent = '0';
                _0x8.textContent = '--';
                _0x4.disabled = true;
                _0x5.disabled = false;
                _0xA = true;

                try {
                    const _0x1A = _0xC.startTask(_0x18, _0x16, _0x17);
                    _0xB.id = _0x1A;
                    _0x12('✅ تم بدء التحليل بنجاح!');
                    _0x14(_0x1A);
                } catch (error) {
                    _0x12('❌ فشل البدء: ' + error.message);
                    _0x13(false);
                }
            });

            _0x5.addEventListener('click', function() {
                _0x13(true);
            });

            window.addEventListener('beforeunload', function(e) {
                if (_0xA) {
                    e.preventDefault();
                    e.returnValue = 'المعالجة لا تزال قيد التنفيذ. هل أنت متأكد من المغادرة؟';
                }
            });

            _0x12('💡 جاهز! أدخل رابط المصدر واضغط "بدء التحليل".');
            _0x12('📌 هذه الأداة تقوم بمحاكاة تحليل بيانات – لا تتفاعل مع أي منصة خارجية.');
        })();
    </script>
</body>
</html>
