<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>职朴通 - 职业赋能平台</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        /* 全局样式 */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', 'Microsoft YaHei', sans-serif;
        }
        
        body {
            background-color: #f8fafc;
            color: #334155;
            line-height: 1.6;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }
        
        /* 导航栏样式 */
        header {
            background-color: #fff;
            box-shadow: 0 2px 15px rgba(0, 0, 0, 0.08);
            position: sticky;
            top: 0;
            z-index: 100;
        }
        
        nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 18px 0;
        }
        
        .logo {
            display: flex;
            align-items: center;
            font-size: 26px;
            font-weight: 700;
            color: #2563eb;
        }
        
        .logo i {
            margin-right: 10px;
            font-size: 28px;
        }
        
        .nav-links {
            display: flex;
            list-style: none;
            align-items: center;
        }
        
        .nav-links li {
            margin-left: 30px;
        }
        
        .nav-links a {
            text-decoration: none;
            color: #475569;
            font-weight: 500;
            transition: color 0.3s;
            position: relative;
        }
        
        .nav-links a:hover {
            color: #2563eb;
        }
        
        .nav-links a::after {
            content: '';
            position: absolute;
            bottom: -5px;
            left: 0;
            width: 0;
            height: 2px;
            background-color: #2563eb;
            transition: width 0.3s;
        }
        
        .nav-links a:hover::after {
            width: 100%;
        }
        
        /* 登录按钮样式 */
        .login-btn {
            background-color: #2563eb;
            color: white;
            border: none;
            padding: 10px 24px;
            border-radius: 20px;
            font-weight: 600;
            cursor: pointer;
            transition: background-color 0.3s, transform 0.3s;
        }
        
        .login-btn:hover {
            background-color: #1d4ed8;
            transform: translateY(-2px);
        }
        
        /* 模态框样式 */
        .modal {
            display: none;
            position: fixed;
            z-index: 1000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            animation: fadeIn 0.3s ease-out;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        
        .modal-content {
            background-color: white;
            margin: 5% auto;
            padding: 0;
            border-radius: 12px;
            width: 90%;
            max-width: 500px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            animation: slideIn 0.3s ease-out;
        }
        
        @keyframes slideIn {
            from { transform: translateY(-50px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }
        
        .modal-header {
            background: linear-gradient(135deg, #2563eb, #3b82f6);
            color: white;
            padding: 25px 30px;
            border-radius: 12px 12px 0 0;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .modal-header h2 {
            font-size: 24px;
            font-weight: 600;
        }
        
        .close {
            color: white;
            font-size: 28px;
            font-weight: bold;
            cursor: pointer;
            transition: transform 0.3s;
        }
        
        .close:hover {
            transform: scale(1.1);
        }
        
        .modal-body {
            padding: 30px;
        }
        
        /* 表单样式 */
        .form-container {
            display: none;
        }
        
        .active-form {
            display: block;
        }
        
        .form-group {
            margin-bottom: 20px;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
            color: #475569;
        }
        
        .form-group input, .form-group select {
            width: 100%;
            padding: 12px 15px;
            border: 1px solid #cbd5e1;
            border-radius: 8px;
            font-size: 16px;
            transition: border-color 0.3s, box-shadow 0.3s;
        }
        
        .form-group input:focus, .form-group select:focus {
            border-color: #2563eb;
            box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.1);
            outline: none;
        }
        
        .form-row {
            display: flex;
            gap: 15px;
        }
        
        .form-row .form-group {
            flex: 1;
        }
        
        .submit-btn {
            background-color: #2563eb;
            color: white;
            border: none;
            padding: 14px 20px;
            border-radius: 8px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            width: 100%;
            transition: background-color 0.3s;
            margin-top: 10px;
        }
        
        .submit-btn:hover {
            background-color: #1d4ed8;
        }
        
        .form-footer {
            text-align: center;
            margin-top: 20px;
            padding-top: 20px;
            border-top: 1px solid #e2e8f0;
        }
        
        .form-footer p {
            color: #64748b;
            margin-bottom: 10px;
        }
        
        .toggle-form {
            color: #2563eb;
            background: none;
            border: none;
            font-weight: 600;
            cursor: pointer;
            font-size: 16px;
            padding: 0;
        }
        
        .toggle-form:hover {
            text-decoration: underline;
        }
        
        /* 用户信息展示 */
        .user-info {
            display: none;
            align-items: center;
            gap: 10px;
        }
        
        .user-avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background-color: #2563eb;
            color: white;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: 600;
        }
        
        .user-name {
            font-weight: 500;
            color: #475569;
        }
        
        .logout-btn {
            background: none;
            border: 1px solid #cbd5e1;
            color: #64748b;
            padding: 6px 12px;
            border-radius: 15px;
            font-size: 14px;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .logout-btn:hover {
            background-color: #f1f5f9;
            color: #334155;
        }
        
        /* 英雄区域样式 */
        .hero {
            background: linear-gradient(135deg, #2563eb, #3b82f6);
            color: white;
            padding: 100px 0;
            text-align: center;
            position: relative;
            overflow: hidden;
        }
        
        .hero::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1440 320"><path fill="%23ffffff" fill-opacity="0.1" d="M0,96L48,112C96,128,192,160,288,186.7C384,213,480,235,576,213.3C672,192,768,128,864,128C960,128,1056,192,1152,192C1248,192,1344,128,1392,96L1440,64L1440,320L1392,320C1344,320,1248,320,1152,320C1056,320,960,320,864,320C768,320,672,320,576,320C480,320,384,320,288,320C192,320,96,320,48,320L0,320Z"></path></svg>');
            background-size: cover;
            background-position: center bottom;
        }
        
        .hero-content {
            position: relative;
            z-index: 1;
        }
        
        .hero h1 {
            font-size: 42px;
            margin-bottom: 20px;
            font-weight: 700;
        }
        
        .hero p {
            font-size: 20px;
            max-width: 700px;
            margin: 0 auto 35px;
            opacity: 0.9;
        }
        
        .cta-button {
            display: inline-block;
            background-color: white;
            color: #2563eb;
            padding: 14px 35px;
            border-radius: 30px;
            text-decoration: none;
            font-weight: 600;
            font-size: 16px;
            transition: transform 0.3s, box-shadow 0.3s;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
        }
        
        .cta-button:hover {
            transform: translateY(-3px);
            box-shadow: 0 7px 20px rgba(0, 0, 0, 0.15);
        }
        
        /* 功能区域样式 */
        .features {
            padding: 100px 0;
        }
        
        .section-title {
            text-align: center;
            margin-bottom: 60px;
        }
        
        .section-title h2 {
            font-size: 36px;
            color: #1e293b;
            margin-bottom: 15px;
            font-weight: 700;
        }
        
        .section-title p {
            color: #64748b;
            max-width: 600px;
            margin: 0 auto;
            font-size: 18px;
        }
        
        .features-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 30px;
        }
        
        .feature-card {
            background-color: white;
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.06);
            transition: transform 0.4s, box-shadow 0.4s;
            display: flex;
            flex-direction: column;
            height: 100%;
        }
        
        .feature-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.1);
        }
        
        .feature-icon {
            background: linear-gradient(135deg, #2563eb, #3b82f6);
            height: 160px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 60px;
            color: white;
        }
        
        .feature-content {
            padding: 30px;
            flex-grow: 1;
            display: flex;
            flex-direction: column;
        }
        
        .feature-content h3 {
            font-size: 22px;
            margin-bottom: 15px;
            color: #1e293b;
        }
        
        .feature-content p {
            color: #64748b;
            margin-bottom: 25px;
            flex-grow: 1;
        }
        
        .feature-button {
            display: inline-block;
            background-color: #f1f5f9;
            color: #2563eb;
            padding: 10px 22px;
            border-radius: 20px;
            text-decoration: none;
            font-size: 14px;
            font-weight: 600;
            transition: background-color 0.3s, color 0.3s;
            text-align: center;
        }
        
        .feature-button:hover {
            background-color: #2563eb;
            color: white;
        }
        
        /* 页脚样式 */
        footer {
            background-color: #1e293b;
            color: #cbd5e1;
            padding: 60px 0 20px;
        }
        
        .footer-content {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 40px;
            margin-bottom: 40px;
        }
        
        .footer-column h3 {
            font-size: 18px;
            margin-bottom: 20px;
            color: #fff;
        }
        
        .footer-links {
            list-style: none;
        }
        
        .footer-links li {
            margin-bottom: 12px;
        }
        
        .footer-links a {
            color: #94a3b8;
            text-decoration: none;
            transition: color 0.3s;
        }
        
        .footer-links a:hover {
            color: #60a5fa;
        }
        
        .copyright {
            text-align: center;
            padding-top: 25px;
            border-top: 1px solid #334155;
            color: #94a3b8;
            font-size: 14px;
        }
        
        /* 响应式设计 */
        @media (max-width: 768px) {
            .nav-links {
                display: none;
            }
            
            .hero h1 {
                font-size: 32px;
            }
            
            .hero p {
                font-size: 18px;
            }
            
            .features-grid {
                grid-template-columns: 1fr;
            }
            
            .form-row {
                flex-direction: column;
                gap: 0;
            }
        }
    </style>
</head>
<body>
    <!-- 导航栏 -->
    <header>
        <div class="container">
            <nav>
                <div class="logo">
                    <i class="fas fa-rocket"></i>
                    职朴通
                </div>
                <ul class="nav-links">
                    <li><a href="#resume">AI简历重塑</a></li>
                    <li><a href="#photo">形象照美化</a></li>
                    <li><a href="#video">展示视频制作</a></li>
                    <li><a href="#interview">面试赋能</a></li>
                    <li><a href="#job">岗位推送</a></li>
                    <li>
                        <div class="user-info" id="userInfo">
                            <div class="user-avatar" id="userAvatar">U</div>
                            <span class="user-name" id="userName">用户</span>
                            <button class="logout-btn" id="logoutBtn">退出</button>
                        </div>
                        <button class="login-btn" id="loginBtn">登录/注册</button>
                    </li>
                </ul>
            </nav>
        </div>
    </header>

    <!-- 登录/注册模态框 -->
    <div id="loginModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 id="modalTitle">登录职朴通</h2>
                <span class="close" id="closeModal">&times;</span>
            </div>
            <div class="modal-body">
                <!-- 登录表单 -->
                <form id="loginForm" class="form-container active-form">
                    <div class="form-group">
                        <label for="loginEmail">邮箱地址</label>
                        <input type="email" id="loginEmail" required placeholder="请输入您的邮箱">
                    </div>
                    <div class="form-group">
                        <label for="loginPassword">密码</label>
                        <input type="password" id="loginPassword" required placeholder="请输入密码">
                    </div>
                    <button type="submit" class="submit-btn">登录</button>
                    <div class="form-footer">
                        <p>还没有账号？ <button type="button" class="toggle-form" data-target="registerForm">立即注册</button></p>
                    </div>
                </form>
                
                <!-- 注册表单 -->
                <form id="registerForm" class="form-container">
                    <div class="form-group">
                        <label for="regName">姓名</label>
                        <input type="text" id="regName" required placeholder="请输入您的姓名">
                    </div>
                    <div class="form-group">
                        <label for="regEmail">邮箱地址</label>
                        <input type="email" id="regEmail" required placeholder="请输入您的邮箱">
                    </div>
                    <div class="form-group">
                        <label for="regPassword">密码</label>
                        <input type="password" id="regPassword" required placeholder="请设置密码（至少6位）">
                    </div>
                    <div class="form-row">
                        <div class="form-group">
                            <label for="regGender">性别</label>
                            <select id="regGender" required>
                                <option value="">请选择</option>
                                <option value="male">男</option>
                                <option value="female">女</option>
                                <option value="other">其他</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label for="regAge">年龄</label>
                            <input type="number" id="regAge" min="18" max="70" required placeholder="年龄">
                        </div>
                    </div>
                    <div class="form-row">
                        <div class="form-group">
                            <label for="regExperience">工龄（年）</label>
                            <input type="number" id="regExperience" min="0" max="50" required placeholder="工作年限">
                        </div>
                        <div class="form-group">
                            <label for="regProfession">职业</label>
                            <select id="regProfession" required>
                                <option value="">请选择职业</option>
                                <option value="it">IT/互联网</option>
                                <option value="finance">金融/会计</option>
                                <option value="education">教育/培训</option>
                                <option value="healthcare">医疗/护理</option>
                                <option value="sales">销售/市场</option>
                                <option value="design">设计/创意</option>
                                <option value="engineering">工程/制造</option>
                                <option value="government">政府/事业单位</option>
                                <option value="other">其他</option>
                            </select>
                        </div>
                    </div>
                    <div class="form-group">
                        <label for="regIndustry">行业</label>
                        <input type="text" id="regIndustry" required placeholder="请输入您所在的行业">
                    </div>
                    <button type="submit" class="submit-btn">注册</button>
                    <div class="form-footer">
                        <p>已有账号？ <button type="button" class="toggle-form" data-target="loginForm">立即登录</button></p>
                    </div>
                </form>
            </div>
        </div>
    </div>

    <!-- 英雄区域 -->
    <section class="hero">
        <div class="container">
            <div class="hero-content">
                <h1>开启职业新篇章，让AI为你的求职赋能</h1>
                <p>一站式职业发展平台，通过AI技术提升你的简历、形象和面试表现，助你找到理想工作</p>
                <a href="#features" class="cta-button">立即体验</a>
            </div>
        </div>
    </section>

    <!-- 功能区域 -->
    <section class="features" id="features">
        <div class="container">
            <div class="section-title">
                <h2>我们的服务</h2>
                <p>全方位职业赋能，从简历到面试，从形象到岗位匹配</p>
            </div>
            
            <div class="features-grid">
                <!-- AI智能简历重塑 -->
                <div class="feature-card" id="resume">
                    <div class="feature-icon">
                        <i class="fas fa-file-alt"></i>
                    </div>
                    <div class="feature-content">
                        <h3>AI智能简历重塑</h3>
                        <p>通过与AI对话，生成一份突出技能和优势的专业简历。我们的AI系统会分析您的背景，优化内容结构，使您的简历更具吸引力。</p>
                        <a href="#" class="feature-button">开始对话</a>
                    </div>
                </div>
                
                <!-- 形象照美化 -->
                <div class="feature-card" id="photo">
                    <div class="feature-icon">
                        <i class="fas fa-camera-retro"></i>
                    </div>
                    <div class="feature-content">
                        <h3>形象照美化</h3>
                        <p>上传您的正脸照片，我们的专业图像处理技术将为您打造一张专业、得体的职业形象照，提升您的专业形象。</p>
                        <a href="#" class="feature-button">上传照片</a>
                    </div>
                </div>
                
                <!-- 个人展示视频制作 -->
                <div class="feature-card" id="video">
                    <div class="feature-icon">
                        <i class="fas fa-video"></i>
                    </div>
                    <div class="feature-content">
                        <h3>个人展示视频制作</h3>
                        <p>按照我们的指导拍摄个人展示视频，我们提供专业的视频剪辑服务，帮助您制作出令人印象深刻的自我介绍视频。</p>
                        <a href="#" class="feature-button">了解详情</a>
                    </div>
                </div>
                
                <!-- 面试赋能 -->
                <div class="feature-card" id="interview">
                    <div class="feature-icon">
                        <i class="fas fa-handshake"></i>
                    </div>
                    <div class="feature-content">
                        <h3>面试赋能</h3>
                        <p>提供模拟面试辅导，包括常见问题解答、面试技巧培训和个性化反馈，帮助您在真实面试中更加自信从容。</p>
                        <a href="#" class="feature-button">预约辅导</a>
                    </div>
                </div>
                
                <!-- 智能岗位推送与曝光 -->
                <div class="feature-card" id="job">
                    <div class="feature-icon">
                        <i class="fas fa-bullseye"></i>
                    </div>
                    <div class="feature-content">
                        <h3>智能岗位推送与曝光</h3>
                        <p>根据您的技能和偏好，智能推荐匹配的岗位机会。同时将您的简历和展示视频推送给合适的雇主，增加就业机会。</p>
                        <a href="#" class="feature-button">查看岗位</a>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- 页脚 -->
    <footer>
        <div class="container">
            <div class="footer-content">
                <div class="footer-column">
                    <h3>职朴通</h3>
                    <ul class="footer-links">
                        <li><a href="#">关于我们</a></li>
                        <li><a href="#">团队介绍</a></li>
                        <li><a href="#">加入我们</a></li>
                    </ul>
                </div>
                <div class="footer-column">
                    <h3>服务</h3>
                    <ul class="footer-links">
                        <li><a href="#resume">AI简历重塑</a></li>
                        <li><a href="#photo">形象照美化</a></li>
                        <li><a href="#video">展示视频制作</a></li>
                        <li><a href="#interview">面试赋能</a></li>
                        <li><a href="#job">岗位推送</a></li>
                    </ul>
                </div>
                <div class="footer-column">
                    <h3>支持</h3>
                    <ul class="footer-links">
                        <li><a href="#">帮助中心</a></li>
                        <li><a href="#">联系我们</a></li>
                        <li><a href="#">隐私政策</a></li>
                        <li><a href="#">服务条款</a></li>
                    </ul>
                </div>
                <div class="footer-column">
                    <h3>联系我们</h3>
                    <ul class="footer-links">
                        <li><i class="fas fa-phone"></i> 400-123-4567</li>
                        <li><i class="fas fa-envelope"></i> contact@zhipt.com</li>
                        <li><i class="fas fa-map-marker-alt"></i> 重庆市北碚区西南大学</li>
                    </ul>
                </div>
            </div>
            <div class="copyright">
                <p>&copy; 2023 职朴通 - 职业赋能平台. 保留所有权利.</p>
            </div>
        </div>
    </footer>

    <script>
        // 登录/注册功能
        document.addEventListener('DOMContentLoaded', function() {
            // 获取DOM元素
            const loginBtn = document.getElementById('loginBtn');
            const logoutBtn = document.getElementById('logoutBtn');
            const loginModal = document.getElementById('loginModal');
            const closeModal = document.getElementById('closeModal');
            const modalTitle = document.getElementById('modalTitle');
            const loginForm = document.getElementById('loginForm');
            const registerForm = document.getElementById('registerForm');
            const toggleButtons = document.querySelectorAll('.toggle-form');
            const userInfo = document.getElementById('userInfo');
            const userAvatar = document.getElementById('userAvatar');
            const userName = document.getElementById('userName');
            
            // 模拟用户数据存储
            let currentUser = null;
            
            // 打开登录模态框
            loginBtn.addEventListener('click', function() {
                loginModal.style.display = 'block';
                showForm('loginForm');
            });
            
            // 关闭登录模态框
            closeModal.addEventListener('click', function() {
                loginModal.style.display = 'none';
            });
            
            // 点击模态框外部关闭
            window.addEventListener('click', function(event) {
                if (event.target === loginModal) {
                    loginModal.style.display = 'none';
                }
            });
            
            // 切换登录/注册表单
            toggleButtons.forEach(button => {
                button.addEventListener('click', function() {
                    const targetForm = this.getAttribute('data-target');
                    showForm(targetForm);
                });
            });
            
            // 显示指定表单
            function showForm(formId) {
                // 隐藏所有表单
                document.querySelectorAll('.form-container').forEach(form => {
                    form.classList.remove('active-form');
                });
                
                // 显示目标表单
                document.getElementById(formId).classList.add('active-form');
                
                // 更新模态框标题
                if (formId === 'loginForm') {
                    modalTitle.textContent = '登录职朴通';
                } else {
                    modalTitle.textContent = '注册职朴通';
                }
            }
            
            // 登录表单提交
            loginForm.addEventListener('submit', function(e) {
                e.preventDefault();
                
                const email = document.getElementById('loginEmail').value;
                const password = document.getElementById('loginPassword').value;
                
                // 简单的验证
                if (!email || !password) {
                    alert('请输入邮箱和密码');
                    return;
                }
                
                // 模拟登录成功
                currentUser = {
                    name: "模拟用户",
                    email: email,
                    avatarText: email.charAt(0).toUpperCase()
                };
                
                // 更新UI显示用户信息
                updateUserUI();
                
                // 关闭模态框
                loginModal.style.display = 'none';
                
                // 清空表单
                loginForm.reset();
                
                alert('登录成功！');
            });
            
            // 注册表单提交
            registerForm.addEventListener('submit', function(e) {
                e.preventDefault();
                
                // 获取表单数据
                const name = document.getElementById('regName').value;
                const email = document.getElementById('regEmail').value;
                const password = document.getElementById('regPassword').value;
                const gender = document.getElementById('regGender').value;
                const age = document.getElementById('regAge').value;
                const experience = document.getElementById('regExperience').value;
                const profession = document.getElementById('regProfession').value;
                const industry = document.getElementById('regIndustry').value;
                
                // 简单验证
                if (!name || !email || !password || !gender || !age || !experience || !profession || !industry) {
                    alert('请填写所有必填字段');
                    return;
                }
                
                if (password.length < 6) {
                    alert('密码长度至少为6位');
                    return;
                }
                
                // 模拟注册成功
                currentUser = {
                    name: name,
                    email: email,
                    avatarText: name.charAt(0).toUpperCase(),
                    gender: gender,
                    age: age,
                    experience: experience,
                    profession: profession,
                    industry: industry
                };
                
                // 更新UI显示用户信息
                updateUserUI();
                
                // 关闭模态框
                loginModal.style.display = 'none';
                
                // 清空表单
                registerForm.reset();
                
                alert(`注册成功！\n\n您的个人信息：\n姓名：${name}\n年龄：${age}\n工龄：${experience}年\n职业：${getProfessionText(profession)}\n行业：${industry}`);
            });
            
            // 获取职业文本
            function getProfessionText(professionCode) {
                const professions = {
                    'it': 'IT/互联网',
                    'finance': '金融/会计',
                    'education': '教育/培训',
                    'healthcare': '医疗/护理',
                    'sales': '销售/市场',
                    'design': '设计/创意',
                    'engineering': '工程/制造',
                    'government': '政府/事业单位',
                    'other': '其他'
                };
                return professions[professionCode] || professionCode;
            }
            
            // 更新用户界面
            function updateUserUI() {
                if (currentUser) {
                    // 显示用户信息，隐藏登录按钮
                    userInfo.style.display = 'flex';
                    loginBtn.style.display = 'none';
                    
                    // 更新用户信息
                    userName.textContent = currentUser.name;
                    userAvatar.textContent = currentUser.avatarText;
                } else {
                    // 显示登录按钮，隐藏用户信息
                    userInfo.style.display = 'none';
                    loginBtn.style.display = 'block';
                }
            }
            
            // 退出登录
            logoutBtn.addEventListener('click', function() {
                currentUser = null;
                updateUserUI();
                alert('您已成功退出登录');
            });
            
            // 页面加载时检查是否有已登录用户
            // 这里可以扩展为从localStorage中读取用户信息
            // 目前只显示登录按钮
            updateUserUI();
        });
    </script>
</body>
</html>
