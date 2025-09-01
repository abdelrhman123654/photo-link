<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>محول الوسائط إلى روابط - النسخة الكاملة</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
    <style>
        :root {
            --primary: #4361ee;
            --secondary: #3a0ca3;
            --accent: #f72585;
            --light: #f8f9fa;
            --dark: #212529;
            --success: #4cc9f0;
            --warning: #ffd166;
            --gray: #adb5bd;
            --dark-bg: #1a1c20;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, var(--dark-bg) 0%, #2d3047 100%);
            color: var(--light);
            min-height: 100vh;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        
        .container {
            width: 100%;
            max-width: 1200px;
            margin: 0 auto;
        }
        
        header {
            text-align: center;
            margin-bottom: 30px;
            width: 100%;
        }
        
        .logo {
            font-size: 2.5rem;
            margin-bottom: 10px;
            color: var(--primary);
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 15px;
        }
        
        .logo-text {
            font-weight: bold;
            background: linear-gradient(45deg, var(--primary), var(--accent));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        
        h1 {
            font-size: 2rem;
            margin-bottom: 15px;
            color: white;
        }
        
        .description {
            font-size: 1.1rem;
            max-width: 600px;
            margin: 0 auto 30px;
            color: rgba(255, 255, 255, 0.8);
            line-height: 1.6;
        }
        
        .server-status {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            margin-bottom: 20px;
            padding: 10px 20px;
            background: rgba(0, 0, 0, 0.2);
            border-radius: 50px;
            width: fit-content;
            margin: 0 auto 30px;
        }
        
        .status-indicator {
            width: 12px;
            height: 12px;
            border-radius: 50%;
            background: var(--success);
            box-shadow: 0 0 10px var(--success);
        }
        
        .upload-container {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 30px;
            width: 100%;
            max-width: 800px;
            margin: 0 auto 30px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .upload-box {
            border: 3px dashed rgba(255, 255, 255, 0.2);
            border-radius: 15px;
            padding: 40px 20px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }
        
        .upload-box:hover {
            border-color: var(--accent);
            background: rgba(255, 255, 255, 0.03);
        }
        
        .upload-box::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: linear-gradient(45deg, transparent, rgba(255, 255, 255, 0.05), transparent);
            transform: rotate(45deg);
            animation: shine 3s infinite;
        }
        
        @keyframes shine {
            0% {
                left: -50%;
            }
            100% {
                left: 150%;
            }
        }
        
        .upload-icon {
            font-size: 4rem;
            margin-bottom: 20px;
            color: var(--warning);
            position: relative;
            z-index: 2;
        }
        
        .upload-text {
            font-size: 1.2rem;
            margin-bottom: 15px;
            position: relative;
            z-index: 2;
        }
        
        .upload-btn {
            background: linear-gradient(45deg, var(--primary), var(--secondary));
            color: white;
            border: none;
            padding: 12px 30px;
            border-radius: 50px;
            font-size: 1rem;
            cursor: pointer;
            transition: all 0.3s ease;
            display: inline-block;
            margin-top: 10px;
            position: relative;
            z-index: 2;
            box-shadow: 0 4px 15px rgba(67, 97, 238, 0.3);
        }
        
        .upload-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(67, 97, 238, 0.4);
        }
        
        .file-types {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 15px;
            margin-top: 30px;
        }
        
        .file-type {
            background: rgba(255, 255, 255, 0.1);
            padding: 12px 20px;
            border-radius: 12px;
            display: flex;
            align-items: center;
            gap: 10px;
            transition: all 0.3s ease;
        }
        
        .file-type:hover {
            background: rgba(255, 255, 255, 0.15);
            transform: translateY(-3px);
        }
        
        .progress-container {
            width: 100%;
            height: 8px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 4px;
            margin: 20px 0;
            overflow: hidden;
            display: none;
        }
        
        .progress-bar {
            height: 100%;
            background: linear-gradient(45deg, var(--primary), var(--accent));
            border-radius: 4px;
            width: 0%;
            transition: width 0.3s ease;
        }
        
        .result-container {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 30px;
            width: 100%;
            max-width: 800px;
            margin: 0 auto;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
            border: 1px solid rgba(255, 255, 255, 0.1);
            display: none;
        }
        
        .result-title {
            text-align: center;
            margin-bottom: 20px;
            color: var(--warning);
            font-size: 1.5rem;
        }
        
        .link-box {
            background: rgba(0, 0, 0, 0.2);
            border-radius: 12px;
            padding: 15px;
            display: flex;
            margin-bottom: 25px;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .link-input {
            flex: 1;
            border: none;
            background: transparent;
            font-size: 1rem;
            padding: 10px 15px;
            color: white;
        }
        
        .copy-btn {
            background: linear-gradient(45deg, var(--primary), var(--secondary));
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .copy-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 10px rgba(67, 97, 238, 0.3);
        }
        
        .qr-container {
            display: flex;
            flex-direction: column;
            align-items: center;
            margin-top: 20px;
        }
        
        #qrcode {
            background: white;
            padding: 15px;
            border-radius: 12px;
            margin-bottom: 20px;
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.2);
        }
        
        .download-btn {
            background: linear-gradient(45deg, var(--success), #3a9fc9);
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            display: inline-flex;
            align-items: center;
            gap: 10px;
            box-shadow: 0 4px 15px rgba(76, 201, 240, 0.3);
        }
        
        .download-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(76, 201, 240, 0.4);
        }
        
        .media-preview {
            width: 100%;
            max-width: 400px;
            margin: 0 auto 25px;
            border-radius: 12px;
            overflow: hidden;
            display: none;
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.3);
        }
        
        .media-preview img, .media-preview video {
            width: 100%;
            display: block;
        }
        
        .media-preview audio {
            width: 100%;
        }
        
        .server-console {
            background: rgba(0, 0, 0, 0.2);
            border-radius: 12px;
            padding: 20px;
            margin: 30px auto;
            width: 100%;
            max-width: 800px;
            font-family: monospace;
            font-size: 0.9rem;
            max-height: 200px;
            overflow-y: auto;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .console-entry {
            margin-bottom: 8px;
            color: var(--success);
        }
        
        .console-entry.error {
            color: var(--accent);
        }
        
        .console-entry.warning {
            color: var(--warning);
        }
        
        .server-info {
            text-align: center;
            margin: 20px 0;
            color: rgba(255, 255, 255, 0.7);
        }
        
        footer {
            margin-top: 50px;
            text-align: center;
            color: rgba(255, 255, 255, 0.6);
            font-size: 0.9rem;
            padding: 20px;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            width: 100%;
        }
        
        @media (max-width: 768px) {
            h1 {
                font-size: 1.7rem;
            }
            
            .upload-container, .result-container {
                padding: 20px;
            }
            
            .upload-box {
                padding: 30px 15px;
            }
            
            .upload-icon {
                font-size: 3rem;
            }
            
            .file-types {
                flex-direction: column;
                align-items: center;
            }
        }
        
        @media (max-width: 480px) {
            h1 {
                font-size: 1.5rem;
            }
            
            .description {
                font-size: 1rem;
            }
            
            .upload-text {
                font-size: 1.1rem;
            }
            
            .link-box {
                flex-direction: column;
                gap: 10px;
            }
            
            .copy-btn {
                width: 100%;
                justify-content: center;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <div class="logo">
                <i class="fas fa-server"></i>
                <span class="logo-text">MediaShare Server</span>
            </div>
            <h1>محول الوسائط إلى روابط</h1>
            <p class="description">
                نظام متكامل لتحويل الصور، الموسيقى والفيديوهات إلى روابط قابلة للمشاركة مع كود QR.
                يتم تخزين الوسائط على خادم آمن ويمكن للآخرين الوصول إليها عبر الرابط.
            </p>
            
            <div class="server-status">
                <div class="status-indicator"></div>
                <span>الخادم يعمل - جاهز لاستقبال الملفات</span>
            </div>
        </header>
        
        <div class="upload-container">
            <div class="upload-box" id="dropArea">
                <i class="fas fa-cloud-upload-alt upload-icon"></i>
                <p class="upload-text">اسحب وأسقط الملف هنا أو انقر للاختيار</p>
                <button class="upload-btn" id="uploadBtn">
                    <i class="fas fa-file-upload"></i> اختر ملف للرفع
                </button>
                <input type="file" id="fileInput" style="display: none;" accept="image/*,video/*,audio/*">
            </div>
            
            <div class="progress-container" id="progressContainer">
                <div class="progress-bar" id="progressBar"></div>
            </div>
            
            <div class="file-types">
                <div class="file-type">
                    <i class="fas fa-image"></i>
                    <span>الصور (JPEG, PNG, GIF, WEBP)</span>
                </div>
                <div class="file-type">
                    <i class="fas fa-music"></i>
                    <span>الموسيقى (MP3, WAV, OGG)</span>
                </div>
                <div class="file-type">
                    <i class="fas fa-video"></i>
                    <span>الفيديو (MP4, MOV, AVI)</span>
                </div>
            </div>
        </div>
        
        <div class="media-preview" id="mediaPreview"></div>
        
        <div class="result-container" id="resultContainer">
            <h2 class="result-title">تم رفع الملف بنجاح إلى الخادم!</h2>
            
            <div class="link-box">
                <input type="text" class="link-input" id="generatedLink" readonly>
                <button class="copy-btn" id="copyBtn">
                    <i class="fas fa-copy"></i> نسخ الرابط
                </button>
            </div>
            
            <div class="qr-container">
                <div id="qrcode"></div>
                <button class="download-btn" id="downloadBtn">
                    <i class="fas fa-download"></i> تحميل QR Code
                </button>
            </div>
        </div>
        
        <div class="server-info">
            <i class="fas fa-database"></i> مساحة التخزين المستخدمة: <span id="storageUsed">0</span> من 100MB
        </div>
        
        <div class="server-console" id="serverConsole">
            <div class="console-entry">[INFO] تم تشغيل الخادم بنجاح</div>
            <div class="console-entry">[INFO] جاهز لاستقبال طلبات الرفع</div>
        </div>
    </div>
    
    <footer>
        <p>© 2023 MediaShare Server. جميع الحقوق محفوظة.</p>
        <p>هذا خادم افتراضي يحاكي عمل الخادم الحقيقي، التخزين يتم محلياً في المتصفح</p>
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const dropArea = document.getElementById('dropArea');
            const fileInput = document.getElementById('fileInput');
            const uploadBtn = document.getElementById('uploadBtn');
            const progressContainer = document.getElementById('progressContainer');
            const progressBar = document.getElementById('progressBar');
            const resultContainer = document.getElementById('resultContainer');
            const mediaPreview = document.getElementById('mediaPreview');
            const generatedLink = document.getElementById('generatedLink');
            const copyBtn = document.getElementById('copyBtn');
            const downloadBtn = document.getElementById('downloadBtn');
            const serverConsole = document.getElementById('serverConsole');
            const storageUsed = document.getElementById('storageUsed');
            let qrcode = null;
            let currentFile = null;
            
            // محاكاة الخادم - بيانات الملفات
            let serverFiles = JSON.parse(localStorage.getItem('serverFiles') || '{}');
            updateStorageUsage();
            
            // إضافة رسالة إلى console الخادم
            function addConsoleMessage(message, type = 'info') {
                const entry = document.createElement('div');
                entry.className = `console-entry ${type}`;
                entry.textContent = `[${new Date().toLocaleTimeString()}] ${message}`;
                serverConsole.appendChild(entry);
                serverConsole.scrollTop = serverConsole.scrollHeight;
            }
            
            // تحديث مساحة التخزين المستخدمة
            function updateStorageUsage() {
                let totalSize = 0;
                for (const id in serverFiles) {
                    totalSize += serverFiles[id].size;
                }
                const usedMB = (totalSize / (1024 * 1024)).toFixed(2);
                storageUsed.textContent = `${usedMB}MB`;
            }
            
            // التعامل مع رفع الملفات
            uploadBtn.addEventListener('click', () => {
                fileInput.click();
            });
            
            fileInput.addEventListener('change', handleFileUpload);
            
            // التعامل مع سحب وإسقاط الملفات
            dropArea.addEventListener('dragover', (e) => {
                e.preventDefault();
                dropArea.style.borderColor = '#f72585';
                dropArea.style.backgroundColor = 'rgba(255, 255, 255, 0.05)';
            });
            
            dropArea.addEventListener('dragleave', () => {
                dropArea.style.borderColor = 'rgba(255, 255, 255, 0.2)';
                dropArea.style.backgroundColor = 'transparent';
            });
            
            dropArea.addEventListener('drop', (e) => {
                e.preventDefault();
                dropArea.style.borderColor = 'rgba(255, 255, 255, 0.2)';
                dropArea.style.backgroundColor = 'transparent';
                
                if (e.dataTransfer.files.length) {
                    fileInput.files = e.dataTransfer.files;
                    handleFileUpload();
                }
            });
            
            // نسخ الرابط
            copyBtn.addEventListener('click', () => {
                generatedLink.select();
                document.execCommand('copy');
                
                const originalText = copyBtn.innerHTML;
                copyBtn.innerHTML = '<i class="fas fa-check"></i> تم النسخ!';
                
                setTimeout(() => {
                    copyBtn.innerHTML = originalText;
                }, 2000);
            });
            
            // تحميل كود QR
            downloadBtn.addEventListener('click', downloadQRCode);
            
            // معالجة رفع الملف إلى الخادم
            function handleFileUpload() {
                if (fileInput.files.length === 0) return;
                
                const file = fileInput.files[0];
                currentFile = file;
                
                // التحقق من حجم الملف (100MB كحد أقصى)
                if (file.size > 100 * 1024 * 1024) {
                    addConsoleMessage(`[ERROR] حجم الملف كبير جداً: ${(file.size/(1024*1024)).toFixed(2)}MB. الحد الأقصى هو 100MB`, 'error');
                    alert('حجم الملف كبير جداً. الحد الأقصى المسموح به هو 100MB');
                    return;
                }
                
                // عرض معاينة الوسائط
                showMediaPreview(file);
                
                // محاكاة الرفع إلى الخادم مع شريط التقدم
                progressContainer.style.display = 'block';
                addConsoleMessage(`[UPLOAD] بدء رفع الملف: ${file.name} (${formatFileSize(file.size)})`);
                
                let progress = 0;
                const uploadInterval = setInterval(() => {
                    progress += Math.random() * 15;
                    if (progress >= 100) {
                        progress = 100;
                        clearInterval(uploadInterval);
                        finishUpload(file);
                    }
                    progressBar.style.width = `${progress}%`;
                }, 200);
            }
            
            // إكمال عملية الرفع
            function finishUpload(file) {
                // إنشاء معرف فريد للملف
                const fileId = generateFileId();
                
                // حفظ الملف في "الخادم" (localStorage)
                const reader = new FileReader();
                reader.onload = function(e) {
                    serverFiles[fileId] = {
                        name: file.name,
                        type: file.type,
                        size: file.size,
                        data: e.target.result,
                        uploadedAt: new Date().toISOString(),
                        views: 0
                    };
                    
                    // حفظ في التخزين المحلي
                    localStorage.setItem('serverFiles', JSON.stringify(serverFiles));
                    
                    // إنشاء رابط للملف
                    const fileUrl = `${window.location.origin}${window.location.pathname}?file=${fileId}`;
                    generatedLink.value = fileUrl;
                    
                    // إنشاء كود QR
                    generateQRCode(fileUrl);
                    
                    // إظهار نتيجة الرفع
                    resultContainer.style.display = 'block';
                    
                    // التمرير إلى النتيجة
                    resultContainer.scrollIntoView({ behavior: 'smooth' });
                    
                    // تحديث مساحة التخزين
                    updateStorageUsage();
                    
                    // إخفاء شريط التقدم
                    setTimeout(() => {
                        progressContainer.style.display = 'none';
                        progressBar.style.width = '0%';
                    }, 1000);
                    
                    addConsoleMessage(`[UPLOAD] تم رفع الملف بنجاح: ${file.name}`, 'success');
                    addConsoleMessage(`[SERVER] تم إنشاء الرابط: ${fileUrl}`);
                };
                reader.readAsDataURL(file);
            }
            
            // عرض معاينة الوسائط
            function showMediaPreview(file) {
                mediaPreview.style.display = 'block';
                mediaPreview.innerHTML = '';
                
                const url = URL.createObjectURL(file);
                const fileType = file.type.split('/')[0];
                
                if (fileType === 'image') {
                    const img = document.createElement('img');
                    img.src = url;
                    img.alt = file.name;
                    mediaPreview.appendChild(img);
                } else if (fileType === 'video') {
                    const video = document.createElement('video');
                    video.src = url;
                    video.controls = true;
                    mediaPreview.appendChild(video);
                } else if (fileType === 'audio') {
                    const audio = document.createElement('audio');
                    audio.src = url;
                    audio.controls = true;
                    mediaPreview.appendChild(audio);
                }
            }
            
            // إنشاء كود QR
            function generateQRCode(text) {
                if (qrcode) {
                    qrcode.clear();
                }
                
                qrcode = new QRCode("qrcode", {
                    text: text,
                    width: 180,
                    height: 180,
                    colorDark : "#000000",
                    colorLight : "#ffffff",
                    correctLevel : QRCode.CorrectLevel.H
                });
            }
            
            // تحميل كود QR
            function downloadQRCode() {
                if (!qrcode) return;
                
                const canvas = document.querySelector("#qrcode canvas");
                const url = canvas.toDataURL("image/png");
                
                const link = document.createElement("a");
                link.download = `qrcode-${currentFile.name}.png`;
                link.href = url;
                link.click();
                
                addConsoleMessage(`[DOWNLOAD] تم تحميل QR Code للفايل: ${currentFile.name}`);
            }
            
            // إنشاء معرف فريد للملف
            function generateFileId() {
                return Math.random().toString(36).substring(2, 10) + 
                       Math.random().toString(36).substring(2, 10);
            }
            
            // تنسيق حجم الملف
            function formatFileSize(bytes) {
                if (bytes < 1024) return bytes + " bytes";
                else if (bytes < 1048576) return (bytes / 1024).toFixed(2) + " KB";
                else return (bytes / 1048576).toFixed(2) + " MB";
            }
            
            // تحميل ملف من الرابط إذا كان موجوداً
            function loadFileFromUrl() {
                const urlParams = new URLSearchParams(window.location.search);
                const fileId = urlParams.get('file');
                
                if (fileId && serverFiles[fileId]) {
                    const file = serverFiles[fileId];
                    
                    // زيادة عدد المشاهدات
                    file.views = (file.views || 0) + 1;
                    localStorage.setItem('serverFiles', JSON.stringify(serverFiles));
                    
                    // عرض المعاينة
                    showMediaPreviewFromData(file);
                    
                    // إنشاء الرابط
                    const fileUrl = `${window.location.origin}${window.location.pathname}?file=${fileId}`;
                    generatedLink.value = fileUrl;
                    
                    // إنشاء كود QR
                    generateQRCode(fileUrl);
                    
                    // إظهار نتيجة الرفع
                    resultContainer.style.display = 'block';
                    
                    addConsoleMessage(`[ACCESS] تم الوصول إلى الملف: ${file.name} من خلال الرابط المباشر`);
                }
            }
            
            // عرض معاينة من البيانات
            function showMediaPreviewFromData(file) {
                mediaPreview.style.display = 'block';
                mediaPreview.innerHTML = '';
                
                const fileType = file.type.split('/')[0];
                
                if (fileType === 'image') {
                    const img = document.createElement('img');
                    img.src = file.data;
                    img.alt = file.name;
                    mediaPreview.appendChild(img);
                } else if (fileType === 'video') {
                    const video = document.createElement('video');
                    video.src = file.data;
                    video.controls = true;
                    mediaPreview.appendChild(video);
                } else if (fileType === 'audio') {
                    const audio = document.createElement('audio');
                    audio.src = file.data;
                    audio.controls = true;
                    mediaPreview.appendChild(audio);
                }
            }
            
            // تهيئة التطبيق
            function initApp() {
                loadFileFromUrl();
                addConsoleMessage('[INFO] تم تهيئة التطبيق بنجاح');
            }
            
            // بدء التشغيل
            initApp();
        });
    </script>
</body>
</html>
