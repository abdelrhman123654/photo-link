<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>محول الوسائط إلى روابط</title>
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
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .logo {
            font-size: 2rem;
            color: var(--primary);
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .auth-buttons {
            display: flex;
            gap: 15px;
        }
        
        .auth-btn {
            background: rgba(255, 255, 255, 0.1);
            color: white;
            border: 1px solid rgba(255, 255, 255, 0.2);
            padding: 8px 20px;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .auth-btn:hover {
            background: var(--primary);
        }
        
        .user-info {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .user-avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: var(--primary);
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
        }
        
        h1 {
            font-size: 2rem;
            margin-bottom: 15px;
            color: white;
            text-align: center;
        }
        
        .description {
            font-size: 1.1rem;
            max-width: 600px;
            margin: 0 auto 30px;
            color: rgba(255, 255, 255, 0.8);
            line-height: 1.6;
            text-align: center;
        }
        
        /* نماذج التسجيل */
        .auth-container {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 30px;
            width: 100%;
            max-width: 500px;
            margin: 50px auto;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
            border: 1px solid rgba(255, 255, 255, 0.1);
            display: none;
        }
        
        .auth-container.active {
            display: block;
        }
        
        .auth-tabs {
            display: flex;
            margin-bottom: 20px;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .auth-tab {
            padding: 10px 20px;
            cursor: pointer;
            opacity: 0.7;
            transition: all 0.3s ease;
        }
        
        .auth-tab.active {
            opacity: 1;
            border-bottom: 2px solid var(--primary);
        }
        
        .auth-form {
            display: none;
        }
        
        .auth-form.active {
            display: block;
        }
        
        .form-group {
            margin-bottom: 20px;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 8px;
            color: rgba(255, 255, 255, 0.8);
        }
        
        .form-group input {
            width: 100%;
            padding: 12px 15px;
            border-radius: 8px;
            border: 1px solid rgba(255, 255, 255, 0.1);
            background: rgba(0, 0, 0, 0.2);
            color: white;
        }
        
        .submit-btn {
            background: linear-gradient(45deg, var(--primary), var(--secondary));
            color: white;
            border: none;
            padding: 12px 20px;
            border-radius: 8px;
            cursor: pointer;
            width: 100%;
            font-size: 1rem;
            transition: all 0.3s ease;
        }
        
        .submit-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 10px rgba(67, 97, 238, 0.3);
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
        }
        
        .upload-box:hover {
            border-color: var(--accent);
            background: rgba(255, 255, 255, 0.03);
        }
        
        .upload-icon {
            font-size: 4rem;
            margin-bottom: 20px;
            color: var(--warning);
        }
        
        .upload-text {
            font-size: 1.2rem;
            margin-bottom: 15px;
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
        
        .result-container.active {
            display: block;
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
        
        .media-preview.active {
            display: block;
        }
        
        .media-preview img, .media-preview video {
            width: 100%;
            display: block;
        }
        
        .media-preview audio {
            width: 100%;
        }
        
        .user-media {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 30px;
            width: 100%;
            max-width: 1000px;
            margin: 30px auto;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
            border: 1px solid rgba(255, 255, 255, 0.1);
            display: none;
        }
        
        .user-media.active {
            display: block;
        }
        
        .media-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }
        
        .media-item {
            background: rgba(0, 0, 0, 0.2);
            border-radius: 12px;
            overflow: hidden;
            transition: all 0.3s ease;
        }
        
        .media-item:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
        }
        
        .media-thumbnail {
            width: 100%;
            height: 150px;
            object-fit: cover;
        }
        
        .audio-thumbnail {
            width: 100%;
            height: 150px;
            background: linear-gradient(45deg, var(--primary), var(--secondary));
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 3rem;
        }
        
        .media-info {
            padding: 15px;
        }
        
        .media-name {
            font-weight: bold;
            margin-bottom: 5px;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }
        
        .media-date {
            font-size: 0.8rem;
            color: rgba(255, 255, 255, 0.6);
        }
        
        .media-actions {
            display: flex;
            gap: 10px;
            margin-top: 10px;
        }
        
        .media-action-btn {
            background: rgba(255, 255, 255, 0.1);
            color: white;
            border: none;
            padding: 5px 10px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 0.8rem;
            display: flex;
            align-items: center;
            gap: 5px;
        }
        
        .media-action-btn:hover {
            background: var(--primary);
        }
        
        .no-media {
            text-align: center;
            padding: 40px;
            color: rgba(255, 255, 255, 0.6);
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
            header {
                flex-direction: column;
                gap: 15px;
            }
            
            .auth-buttons {
                width: 100%;
                justify-content: center;
            }
            
            h1 {
                font-size: 1.7rem;
            }
            
            .upload-container, .result-container, .auth-container {
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
            
            .media-grid {
                grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
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
            
            .media-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <div class="logo">
                <i class="fas fa-server"></i>
                <span>MediaShare</span>
            </div>
            
            <div class="auth-buttons" id="authButtons">
                <button class="auth-btn" id="showRegister">إنشاء حساب</button>
                <button class="auth-btn" id="showLogin">تسجيل الدخول</button>
            </div>
            
            <div class="user-info" id="userInfo" style="display: none;">
                <div class="user-avatar" id="userAvatar">U</div>
                <span id="userName">مستخدم</span>
                <button class="auth-btn" id="logoutBtn">تسجيل الخروج</button>
            </div>
        </header>
        
        <h1 id="mainTitle">محول الوسائط إلى روابط</h1>
        <p class="description" id="mainDescription">
            قم بتحويل صورك، مقاطع الفيديو والموسيقى إلى روابط قابلة للمشاركة مع كود QR.
        </p>
        
        <!-- نموذج التسجيل -->
        <div class="auth-container" id="authContainer">
            <div class="auth-tabs">
                <div class="auth-tab active" data-tab="register">إنشاء حساب</div>
                <div class="auth-tab" data-tab="login">تسجيل الدخول</div>
            </div>
            
            <form class="auth-form active" id="registerForm">
                <div class="form-group">
                    <label for="registerName">الاسم</label>
                    <input type="text" id="registerName" required>
                </div>
                <div class="form-group">
                    <label for="registerEmail">البريد الإلكتروني</label>
                    <input type="email" id="registerEmail" required>
                </div>
                <div class="form-group">
                    <label for="registerPassword">كلمة المرور</label>
                    <input type="password" id="registerPassword" required>
                </div>
                <button type="submit" class="submit-btn">إنشاء حساب</button>
            </form>
            
            <form class="auth-form" id="loginForm">
                <div class="form-group">
                    <label for="loginEmail">البريد الإلكتروني</label>
                    <input type="email" id="loginEmail" required>
                </div>
                <div class="form-group">
                    <label for="loginPassword">كلمة المرور</label>
                    <input type="password" id="loginPassword" required>
                </div>
                <button type="submit" class="submit-btn">تسجيل الدخول</button>
            </form>
        </div>
        
        <!-- واجهة الرفع -->
        <div class="upload-container" id="uploadContainer">
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
            <h2 class="result-title">تم رفع الملف بنجاح!</h2>
            
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
        
        <!-- وسائط المستخدم -->
        <div class="user-media" id="userMedia">
            <h2>وسائطك</h2>
            <div class="media-grid" id="mediaGrid">
                <!-- سيتم ملء هذا القسم بالوسائط -->
            </div>
        </div>
    </div>
    
    <footer>
        <p>© 2023 MediaShare. جميع الحقوق محفوظة.</p>
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // عناصر DOM
            const authButtons = document.getElementById('authButtons');
            const userInfo = document.getElementById('userInfo');
            const userAvatar = document.getElementById('userAvatar');
            const userName = document.getElementById('userName');
            const showRegister = document.getElementById('showRegister');
            const showLogin = document.getElementById('showLogin');
            const logoutBtn = document.getElementById('logoutBtn');
            const authContainer = document.getElementById('authContainer');
            const loginForm = document.getElementById('loginForm');
            const registerForm = document.getElementById('registerForm');
            const uploadContainer = document.getElementById('uploadContainer');
            const userMedia = document.getElementById('userMedia');
            const mainTitle = document.getElementById('mainTitle');
            const mainDescription = document.getElementById('mainDescription');
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
            const mediaGrid = document.getElementById('mediaGrid');
            const authTabs = document.querySelectorAll('.auth-tab');
            
            let qrcode = null;
            let currentUser = null;
            
            // تهيئة التطبيق
            initApp();
            
            // أحداث التسجيل والدخول
            showRegister.addEventListener('click', () => {
                authContainer.classList.add('active');
                switchAuthTab('register');
            });
            
            showLogin.addEventListener('click', () => {
                authContainer.classList.add('active');
                switchAuthTab('login');
            });
            
            authTabs.forEach(tab => {
                tab.addEventListener('click', () => {
                    const tabName = tab.getAttribute('data-tab');
                    switchAuthTab(tabName);
                });
            });
            
            registerForm.addEventListener('submit', function(e) {
                e.preventDefault();
                const name = document.getElementById('registerName').value;
                const email = document.getElementById('registerEmail').value;
                const password = document.getElementById('registerPassword').value;
                
                registerUser(name, email, password);
            });
            
            loginForm.addEventListener('submit', function(e) {
                e.preventDefault();
                const email = document.getElementById('loginEmail').value;
                const password = document.getElementById('loginPassword').value;
                
                loginUser(email, password);
            });
            
            logoutBtn.addEventListener('click', logoutUser);
            
            // أحداث رفع الملفات
            uploadBtn.addEventListener('click', () => {
                // إذا لم يكن المستخدم مسجلاً، عرض نموذج التسجيل
                if (!currentUser) {
                    authContainer.classList.add('active');
                    return;
                }
                
                fileInput.click();
            });
            
            fileInput.addEventListener('change', handleFileUpload);
            
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
                
                // إذا لم يكن المستخدم مسجلاً، عرض نموذج التسجيل
                if (!currentUser) {
                    authContainer.classList.add('active');
                    return;
                }
                
                if (e.dataTransfer.files.length) {
                    fileInput.files = e.dataTransfer.files;
                    handleFileUpload();
                }
            });
            
            copyBtn.addEventListener('click', () => {
                generatedLink.select();
                document.execCommand('copy');
                
                const originalText = copyBtn.innerHTML;
                copyBtn.innerHTML = '<i class="fas fa-check"></i> تم النسخ!';
                
                setTimeout(() => {
                    copyBtn.innerHTML = originalText;
                }, 2000);
            });
            
            downloadBtn.addEventListener('click', downloadQRCode);
            
            // وظائف التطبيق
            function initApp() {
                // التحقق من وجود مستخدم مسجل دخوله
                const loggedInUser = localStorage.getItem('currentUser');
                if (loggedInUser) {
                    currentUser = JSON.parse(loggedInUser);
                    showUserInterface();
                }
                
                // تحميل الملف من الرابط إذا كان موجوداً
                loadFileFromUrl();
            }
            
            function switchAuthTab(tabName) {
                document.querySelectorAll('.auth-tab').forEach(tab => {
                    tab.classList.remove('active');
                });
                
                document.querySelectorAll('.auth-form').forEach(form => {
                    form.classList.remove('active');
                });
                
                document.querySelector(`.auth-tab[data-tab="${tabName}"]`).classList.add('active');
                document.getElementById(`${tabName}Form`).classList.add('active');
            }
            
            function registerUser(name, email, password) {
                // الحصول على المستخدمين الحاليين
                const users = JSON.parse(localStorage.getItem('users') || '[]');
                
                // التحقق من عدم وجود مستخدم بنفس البريد
                if (users.some(user => user.email === email)) {
                    alert('هذا البريد الإلكتروني مسجل بالفعل');
                    return;
                }
                
                // إنشاء مستخدم جديد
                const newUser = {
                    id: Date.now().toString(),
                    name,
                    email,
                    password, // في تطبيق حقيقي يجب تشفير كلمة المرور
                    createdAt: new Date().toISOString()
                };
                
                // حفظ المستخدم
                users.push(newUser);
                localStorage.setItem('users', JSON.stringify(users));
                
                // تسجيل الدخول تلقائياً
                currentUser = newUser;
                localStorage.setItem('currentUser', JSON.stringify(newUser));
                
                // إظهار واجهة المستخدم
                showUserInterface();
                
                // إخفاء نموذج التسجيل
                authContainer.classList.remove('active');
                
                alert('تم إنشاء حسابك بنجاح!');
            }
            
            function loginUser(email, password) {
                // الحصول على المستخدمين
                const users = JSON.parse(localStorage.getItem('users') || '[]');
                
                // البحث عن المستخدم
                const user = users.find(u => u.email === email && u.password === password);
                
                if (user) {
                    // تسجيل الدخول
                    currentUser = user;
                    localStorage.setItem('currentUser', JSON.stringify(user));
                    
                    // إظهار واجهة المستخدم
                    showUserInterface();
                    
                    // إخفاء نموذج التسجيل
                    authContainer.classList.remove('active');
                } else {
                    alert('البريد الإلكتروني أو كلمة المرور غير صحيحة');
                }
            }
            
            function logoutUser() {
                currentUser = null;
                localStorage.removeItem('currentUser');
                
                // إظهار واجهة التسجيل
                authButtons.style.display = 'flex';
                userInfo.style.display = 'none';
                userMedia.classList.remove('active');
                resultContainer.classList.remove('active');
                
                // إعادة تعيين النصوص الرئيسية
                mainTitle.textContent = 'محول الوسائط إلى روابط';
                mainDescription.textContent = 'قم بتحويل صورك، مقاطع الفيديو والموسيقى إلى روابط قابلة للمشاركة مع كود QR.';
            }
            
            function showUserInterface() {
                // إظهار معلومات المستخدم
                authButtons.style.display = 'none';
                userInfo.style.display = 'flex';
                userAvatar.textContent = currentUser.name.charAt(0);
                userName.textContent = currentUser.name;
                
                // إظهار واجهة الوسائط
                userMedia.classList.add('active');
                
                // تحديث النصوص الرئيسية
                mainTitle.textContent = `مرحباً ${currentUser.name}`;
                mainDescription.textContent = 'يمكنك الآن رفع الوسائط وإنشاء روابط قابلة للمشاركة.';
                
                // تحميل وسائط المستخدم
                loadUserMedia();
            }
            
            function handleFileUpload() {
                if (fileInput.files.length === 0) return;
                
                const file = fileInput.files[0];
                
                // التحقق من حجم الملف (50MB كحد أقصى)
                if (file.size > 50 * 1024 * 1024) {
                    alert('حجم الملف كبير جداً. الحد الأقصى المسموح به هو 50MB');
                    return;
                }
                
                // عرض معاينة الوسائط
                showMediaPreview(file);
                
                // محاكاة المعالجة مع شريط التقدم
                progressContainer.style.display = 'block';
                
                let progress = 0;
                const uploadInterval = setInterval(() => {
                    progress += Math.random() * 15;
                    if (progress >= 100) {
                        progress = 100;
                        clearInterval(uploadInterval);
                        saveUserFile(file);
                    }
                    progressBar.style.width = `${progress}%`;
                }, 200);
            }
            
            function showMediaPreview(file) {
                mediaPreview.classList.add('active');
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
            
            function saveUserFile(file) {
                // تحويل الملف إلى base64
                const reader = new FileReader();
                reader.onload = function(e) {
                    // إنشاء كائن الملف
                    const fileData = {
                        id: Date.now().toString(),
                        name: file.name,
                        type: file.type,
                        size: file.size,
                        data: e.target.result,
                        uploadedAt: new Date().toISOString(),
                        userId: currentUser.id
                    };
                    
                    // الحصول على ملفات المستخدم الحالية
                    const userFiles = JSON.parse(localStorage.getItem('userFiles') || '[]');
                    
                    // إضافة الملف الجديد
                    userFiles.push(fileData);
                    localStorage.setItem('userFiles', JSON.stringify(userFiles));
                    
                    // إنشاء رابط للملف
                    const fileUrl = `${window.location.origin}${window.location.pathname}?file=${fileData.id}`;
                    generatedLink.value = fileUrl;
                    
                    // إنشاء كود QR
                    generateQRCode(fileUrl);
                    
                    // إظهار نتيجة الرفع
                    resultContainer.classList.add('active');
                    
                    // إخفاء شريط التقدم
                    setTimeout(() => {
                        progressContainer.style.display = 'none';
                        progressBar.style.width = '0%';
                    }, 1000);
                    
                    // إعادة تحميل وسائط المستخدم
                    loadUserMedia();
                };
                reader.readAsDataURL(file);
            }
            
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
            
            function downloadQRCode() {
                if (!qrcode) return;
                
                const canvas = document.querySelector("#qrcode canvas");
                const url = canvas.toDataURL("image/png");
                
                const link = document.createElement("a");
                link.download = `qrcode.png`;
                link.href = url;
                link.click();
            }
            
            function loadUserMedia() {
                // الحصول على جميع الملفات
                const allFiles = JSON.parse(localStorage.getItem('userFiles') || '[]');
                
                // تصفية ملفات المستخدم الحالي
                const userFiles = allFiles.filter(file => file.userId === currentUser.id);
                
                // عرض الملفات
                mediaGrid.innerHTML = '';
                
                if (userFiles.length === 0) {
                    mediaGrid.innerHTML = `
                        <div class="no-media">
                            <i class="fas fa-folder-open" style="font-size: 3rem; margin-bottom: 15px;"></i>
                            <p>لا توجد وسائط مرفوعة بعد</p>
                        </div>
                    `;
                    return;
                }
                
                // عرض الملفات بترتيب زمني (الأحدث أولاً)
                userFiles.sort((a, b) => new Date(b.uploadedAt) - new Date(a.uploadedAt));
                
                userFiles.forEach(file => {
                    const fileType = file.type.split('/')[0];
                    const uploadedDate = new Date(file.uploadedAt).toLocaleDateString('ar-EG');
                    
                    const mediaItem = document.createElement('div');
                    mediaItem.className = 'media-item';
                    
                    let thumbnailHTML = '';
                    if (fileType === 'image') {
                        thumbnailHTML = `<img src="${file.data}" class="media-thumbnail" alt="${file.name}">`;
                    } else if (fileType === 'video') {
                        thumbnailHTML = `
                            <video class="media-thumbnail">
                                <source src="${file.data}" type="${file.type}">
                                متصفحك لا يدعم تشغيل الفيديو
                            </video>
                        `;
                    } else {
                        thumbnailHTML = `
                            <div class="audio-thumbnail">
                                <i class="fas fa-music"></i>
                            </div>
                        `;
                    }
                    
                    mediaItem.innerHTML = `
                        ${thumbnailHTML}
                        <div class="media-info">
                            <div class="media-name">${file.name}</div>
                            <div class="media-date">${uploadedDate}</div>
                            <div class="media-actions">
                                <button class="media-action-btn view-btn" data-fileid="${file.id}">
                                    <i class="fas fa-eye"></i> عرض
                                </button>
                                <button class="media-action-btn share-btn" data-fileid="${file.id}">
                                    <i class="fas fa-share"></i> مشاركة
                                </button>
                            </div>
                        </div>
                    `;
                    
                    mediaGrid.appendChild(mediaItem);
                });
                
                // إضافة مستمعي الأحداث لأزرار العرض والمشاركة
                document.querySelectorAll('.view-btn').forEach(btn => {
                    btn.addEventListener('click', function() {
                        const fileId = this.getAttribute('data-fileid');
                        viewFile(fileId);
                    });
                });
                
                document.querySelectorAll('.share-btn').forEach(btn => {
                    btn.addEventListener('click', function() {
                        const fileId = this.getAttribute('data-fileid');
                        shareFile(fileId);
                    });
                });
            }
            
            function viewFile(fileId) {
                // الحصول على جميع الملفات
                const allFiles = JSON.parse(localStorage.getItem('userFiles') || '[]');
                
                // البحث عن الملف
                const file = allFiles.find(f => f.id === fileId);
                
                if (file) {
                    // عرض المعاينة
                    showMediaPreviewFromData(file);
                    
                    // إنشاء الرابط
                    const fileUrl = `${window.location.origin}${window.location.pathname}?file=${file.id}`;
                    generatedLink.value = fileUrl;
                    
                    // إنشاء كود QR
                    generateQRCode(fileUrl);
                    
                    // إظهار نتيجة الرفع
                    resultContainer.classList.add('active');
                    
                    // التمرير إلى الأعلى
                    window.scrollTo({ top: 0, behavior: 'smooth' });
                }
            }
            
            function shareFile(fileId) {
                // الحصول على جميع الملفات
                const allFiles = JSON.parse(localStorage.getItem('userFiles') || '[]');
                
                // البحث عن الملف
                const file = allFiles.find(f => f.id === fileId);
                
                if (file) {
                    // إنشاء الرابط
                    const fileUrl = `${window.location.origin}${window.location.pathname}?file=${file.id}`;
                    
                    // نسخ الرابط إلى الحافظة
                    navigator.clipboard.writeText(fileUrl).then(() => {
                        alert('تم نسخ الرابط إلى الحافظة، يمكنك الآن مشاركته');
                    });
                }
            }
            
            function showMediaPreviewFromData(file) {
                mediaPreview.classList.add('active');
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
            
            // تحميل ملف من الرابط إذا كان موجوداً
            function loadFileFromUrl() {
                const urlParams = new URLSearchParams(window.location.search);
                const fileId = urlParams.get('file');
                
                if (fileId) {
                    // الحصول على جميع الملفات
                    const allFiles = JSON.parse(localStorage.getItem('userFiles') || '[]');
                    
                    // البحث عن الملف
                    const file = allFiles.find(f => f.id === fileId);
                    
                    if (file) {
                        // عرض المعاينة
                        showMediaPreviewFromData(file);
                        
                        // إنشاء الرابط
                        const fileUrl = `${window.location.origin}${window.location.pathname}?file=${file.id}`;
                        generatedLink.value = fileUrl;
                        
                        // إنشاء كود QR
                        generateQRCode(fileUrl);
                        
                        // إظهار نتيجة الرفع
                        resultContainer.classList.add('active');
                    }
                }
            }
        });
    </script>
</body>
</html>
