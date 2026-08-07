<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes, maximum-scale=2.0">
  <title> 个人空间</title>
  <!-- 完全符合 GitHub.io 静态页面标准，纯冷色调、简洁设计 -->
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      background: #0f172a; /* 深邃冷灰蓝底 */
      font-family: 'Inter', 'Segoe UI', 'Roboto', system-ui, -apple-system, sans-serif;
      color: #e2e8f0;
      line-height: 1.5;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      padding: 0 1.5rem;
      letter-spacing: 0.01em;
    }

    /* 冷色调主容器：冰川蓝灰、石板色系 */
    .wrapper {
      max-width: 1100px;
      margin: 0 auto;
      width: 100%;
      flex: 1;
      display: flex;
      flex-direction: column;
    }

    /* ----- 导航栏：右上角布局，冷峻极简 ----- */
    .navbar {
      display: flex;
      justify-content: flex-end;
      align-items: center;
      padding: 1.8rem 0 1.2rem;
      border-bottom: 1px solid rgba(148, 163, 184, 0.15);
      margin-bottom: 2.5rem;
      flex-wrap: wrap;
      gap: 1.2rem;
    }

    /* 头像：圆形，冷色光晕，点击回到主页 */
    .avatar-link {
      display: flex;
      align-items: center;
      justify-content: center;
      text-decoration: none;
      transition: transform 0.2s ease, filter 0.2s;
      margin-right: auto; /* 让头像靠左，菜单整体右对齐？要求右上角包含头像和菜单，所以头像在最左侧，菜单在右侧，整体在右上区域 */
    }
    /* 重新调整：要求右上角包含头像和菜单，典型的 header 右对齐风格。
       这里把头像放在右侧最前面，菜单紧随其后，整体靠右。 */
    .navbar {
      justify-content: flex-end; 
    }
    .avatar-link {
      margin-right: 0; 
      order: 0;
    }

    .avatar-img {
      width: 44px;
      height: 44px;
      border-radius: 50%;
      object-fit: cover;
      border: 2px solid #475569;
      background: #1e293b;
      transition: border-color 0.25s, box-shadow 0.25s;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.4);
      cursor: pointer;
    }

    .avatar-link:hover .avatar-img {
      border-color: #94a3b8;
      box-shadow: 0 0 14px rgba(148, 163, 184, 0.5);
      transform: scale(1.02);
    }

    /* 菜单容器：冷色调文字，菜单项排列 */
    .nav-menu {
      display: flex;
      align-items: center;
      gap: 1.8rem;
      flex-wrap: wrap;
      background: transparent;
    }

    .nav-item {
      color: #94a3b8;
      text-decoration: none;
      font-size: 1rem;
      font-weight: 450;
      letter-spacing: 0.03em;
      padding: 0.4rem 0.2rem;
      position: relative;
      transition: color 0.2s ease;
      white-space: nowrap;
    }

    .nav-item::after {
      content: '';
      position: absolute;
      bottom: 0;
      left: 0;
      width: 0%;
      height: 1.5px;
      background: #cbd5e1;
      transition: width 0.25s ease;
    }

    .nav-item:hover {
      color: #f1f5f9;
    }

    .nav-item:hover::after {
      width: 100%;
    }

    /* 私信按钮特殊一点，但保持冷色 */
    .nav-item.message-link {
      color: #b9c7dd;
      font-weight: 480;
    }

    /* 响应式：小屏菜单换行 */
    @media (max-width: 600px) {
      .navbar {
        justify-content: flex-end;
        gap: 1rem;
      }
      .nav-menu {
        gap: 1rem;
      }
      .avatar-img {
        width: 40px;
        height: 40px;
      }
    }

    /* ----- 主页卡片：个人信息展示区 ----- */
    .home-section {
      flex: 1;
      display: flex;
      flex-direction: column;
      justify-content: center;
      margin-top: 1rem;
    }

    .info-card {
      background: rgba(30, 41, 59, 0.7); /* 冷半透明 slate 800 */
      backdrop-filter: blur(10px);
      -webkit-backdrop-filter: blur(10px);
      border: 1px solid rgba(71, 85, 105, 0.5);
      border-radius: 1.8rem;
      padding: 2.5rem 2.8rem;
      box-shadow: 0 20px 35px -8px rgba(0, 0, 0, 0.5), 0 0 0 1px rgba(255, 255, 255, 0.03);
      max-width: 680px;
      width: 100%;
      transition: border-color 0.3s;
    }

    .info-card:hover {
      border-color: rgba(148, 163, 184, 0.6);
    }

    .greeting {
      font-size: 1rem;
      text-transform: uppercase;
      letter-spacing: 0.2em;
      color: #64748b;
      margin-bottom: 0.8rem;
      font-weight: 500;
    }

    .name {
      font-size: 2.8rem;
      font-weight: 500;
      color: #f8fafc;
      margin-bottom: 0.5rem;
      line-height: 1.2;
      letter-spacing: -0.02em;
    }

    .title-badge {
      display: inline-block;
      background: #1e293b;
      color: #b9c7dd;
      padding: 0.25rem 1rem;
      border-radius: 2rem;
      font-size: 0.9rem;
      font-weight: 450;
      margin: 0.5rem 0 1.5rem;
      border: 1px solid #334155;
      letter-spacing: 0.02em;
    }

    .bio {
      font-size: 1.1rem;
      color: #cbd5e1;
      margin: 1.2rem 0 1.8rem;
      line-height: 1.7;
      border-left: 3px solid #475569;
      padding-left: 1.2rem;
    }

    .details-grid {
      display: flex;
      flex-wrap: wrap;
      gap: 1.8rem;
      margin-top: 1.5rem;
      border-top: 1px solid rgba(148, 163, 184, 0.2);
      padding-top: 1.8rem;
    }

    .detail-item {
      display: flex;
      flex-direction: column;
      gap: 0.2rem;
    }

    .detail-label {
      font-size: 0.8rem;
      text-transform: uppercase;
      letter-spacing: 0.1em;
      color: #64748b;
      font-weight: 500;
    }

    .detail-value {
      font-size: 1.1rem;
      color: #e2e8f0;
      font-weight: 450;
    }

    .location, .contact {
      display: flex;
      align-items: center;
      gap: 0.3rem;
    }

    .social-links {
      margin-top: 2rem;
      display: flex;
      gap: 1.2rem;
      align-items: center;
      color: #94a3b8;
    }

    .social-icon {
      color: #94a3b8;
      text-decoration: none;
      font-size: 0.95rem;
      border-bottom: 1px dashed transparent;
      transition: color 0.2s, border-color 0.2s;
      font-weight: 430;
    }

    .social-icon:hover {
      color: #e2e8f0;
      border-bottom: 1px dashed #94a3b8;
    }

    /* 页脚简约 */
    .footer-note {
      text-align: right;
      font-size: 0.8rem;
      color: #475569;
      padding: 2rem 0 1.2rem;
      border-top: 1px solid rgba(71, 85, 105, 0.3);
      margin-top: 2.5rem;
    }

    button, .nav-item {
      background: none;
      border: none;
      cursor: pointer;
    }

    /* 占位内容样式 (文章/音乐/工作/私信 - 后续通过简单js切换) */
    .placeholder-content {
      background: rgba(30, 41, 59, 0.5);
      backdrop-filter: blur(8px);
      border-radius: 1.5rem;
      padding: 2.5rem;
      color: #cbd5e1;
      border: 1px solid #334155;
      margin-top: 1rem;
      max-width: 680px;
    }

    .hidden-section {
      display: none;
    }

    .active-section {
      display: block;
    }

    .home-link-active {
      color: #f1f5f9;
      font-weight: 500;
    }
  </style>
</head>
<body>
  <div class="wrapper">
    <!-- 导航栏：右上角区域包含头像和菜单 -->
    <header class="navbar">
      <!-- 头像点击返回主页，位于右上角区域的最左侧（视觉上在菜单前面） -->
      <a href="#" class="avatar-link" id="homeAvatarLink" title="回到主页">
        <!-- 头像图片：使用一个冷色调抽象头像，可替换为你的图片链接 -->
        <img 
          src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='100' height='100' viewBox='0 0 100 100'%3E%3Ccircle cx='50' cy='50' r='50' fill='%231e293b'/%3E%3Ccircle cx='50' cy='38' r='18' fill='%23475569'/%3E%3Cellipse cx='50' cy='80' rx='32' ry='20' fill='%23475569'/%3E%3Ccircle cx='38' cy='34' r='4' fill='%23cbd5e1'/%3E%3Ccircle cx='62' cy='34' r='4' fill='%23cbd5e1'/%3E%3Cpath d='M44 44 Q50 50 56 44' stroke='%2394a3b8' stroke-width='3' fill='none' stroke-linecap='round' /%3E%3C/svg%3E"
          alt="用户头像" 
          class="avatar-img"
          loading="lazy"
        >
      </a>

      <!-- 菜单：文章分享、音乐推荐、工作相关、私信 -->
      <nav class="nav-menu" id="mainMenu">
        <a href="#" class="nav-item" data-section="articles">文章分享</a>
        <a href="#" class="nav-item" data-section="music">音乐推荐</a>
        <a href="#" class="nav-item" data-section="work">工作相关</a>
        <a href="#" class="nav-item message-link" data-section="messages">私信</a>
      </nav>
    </header>

    <!-- 主要内容区域：动态切换 -->
    <main id="contentArea">
      <!-- 默认主页 (个人信息) 可见 -->
      <section id="homeSection" class="home-section active-section">
        <div class="info-card">
          <div class="greeting">✦ 个人主页</div>
          <h1 class="name">林寒屿</h1>
          <span class="title-badge">产品设计师 / 数字游民</span>
          <p class="bio">
            栖身于冷冽与理性之间，探索交互的边界。<br>
            目前专注于设计系统、冰川徒步与氛围音乐。
          </p>
          <div class="details-grid">
            <div class="detail-item">
              <span class="detail-label">所在地</span>
              <span class="detail-value location">🇮🇸 雷克雅未克</span>
            </div>
            <div class="detail-item">
              <span class="detail-label">联系</span>
              <span class="detail-value contact">hi@hanyu.design</span>
            </div>
            <div class="detail-item">
              <span class="detail-label">状态</span>
              <span class="detail-value">开放合作 · 远程</span>
            </div>
          </div>
          <div class="social-links">
            <a href="#" class="social-icon">GitHub</a>
            <a href="#" class="social-icon">Dribbble</a>
            <a href="#" class="social-icon">Telegram</a>
          </div>
        </div>
      </section>

      <!-- 文章分享占位 -->
      <section id="articlesSection" class="placeholder-content hidden-section">
        <h2 style="color: #e2e8f0; margin-bottom: 1.2rem; font-weight: 500;">📄 文章分享</h2>
        <ul style="list-style: none; color: #b9c7dd;">
          <li style="margin-bottom: 0.8rem;">◦ 冷色调UI中的视觉平衡 <span style="color: #64748b; margin-left: 1rem;">2026-03-12</span></li>
          <li style="margin-bottom: 0.8rem;">◦ 从冰岛建筑到设计语言 <span style="color: #64748b; margin-left: 1rem;">2026-02-28</span></li>
          <li style="margin-bottom: 0.8rem;">◦ 远程工作的仪式感 <span style="color: #64748b; margin-left: 1rem;">2026-01-15</span></li>
        </ul>
        <p style="margin-top: 2rem; color: #64748b; font-style: italic;">更多文章即将更新...</p>
      </section>

      <!-- 音乐推荐占位 -->
      <section id="musicSection" class="placeholder-content hidden-section">
        <h2 style="color: #e2e8f0; margin-bottom: 1.2rem; font-weight: 500;">🎵 音乐推荐</h2>
        <div style="display: flex; gap: 1.2rem; flex-wrap: wrap;">
          <span style="background:#1e293b; padding:0.4rem 1rem; border-radius:2rem;">❄️ 氛围电子</span>
          <span style="background:#1e293b; padding:0.4rem 1rem; border-radius:2rem;">🌊 后摇</span>
          <span style="background:#1e293b; padding:0.4rem 1rem; border-radius:2rem;">🎹 新古典</span>
        </div>
        <p style="margin-top: 1.5rem; color: #94a3b8;">本周推荐：Hugar · 《Varða》</p>
      </section>

      <!-- 工作相关占位 -->
      <section id="workSection" class="placeholder-content hidden-section">
        <h2 style="color: #e2e8f0; margin-bottom: 1.2rem; font-weight: 500;">⚙️ 工作相关</h2>
        <p style="color: #cbd5e1;">目前就职于 <strong style="color:#f1f5f9;">Nordic Studio</strong> ，担任高级产品设计师。</p>
        <p style="color: #94a3b8; margin-top: 0.8rem;">擅长设计系统、Figma 插件开发、冷调视觉。</p>
        <p style="color: #64748b; margin-top: 2rem;">📧 合作联系：work@hanyu.design</p>
      </section>

      <!-- 私信占位 -->
      <section id="messagesSection" class="placeholder-content hidden-section">
        <h2 style="color: #e2e8f0; margin-bottom: 1.2rem; font-weight: 500;">✉️ 私信</h2>
        <div style="background:#0f172a; border-radius:1rem; padding:1.2rem; border:1px solid #334155;">
          <p style="color: #94a3b8;">发送消息给林寒屿：</p>
          <div style="margin-top:1rem; display:flex; gap:0.5rem; flex-wrap:wrap;">
            <input type="text" placeholder="你的名字" style="background:#1e293b; border:1px solid #475569; padding:0.6rem; border-radius:0.8rem; color:#e2e8f0; width:100%;" disabled>
            <textarea placeholder="写下内容..." rows="3" style="background:#1e293b; border:1px solid #475569; padding:0.6rem; border-radius:0.8rem; color:#e2e8f0; width:100%; margin-top:0.5rem;" disabled></textarea>
            <button style="background:#334155; border:none; color:#e2e8f0; padding:0.5rem 1.5rem; border-radius:2rem; margin-top:0.5rem; opacity:0.8;" disabled>发送</button>
          </div>
          <p style="font-size:0.8rem; color:#475569; margin-top:1rem;">（演示界面，私信功能需后端支持）</p>
        </div>
      </section>
    </main>

    <footer class="footer-note">
      © 2026 寒屿 · 冷色调栖息
    </footer>
  </div>

  <!-- 简单的页面切换脚本，纯前端，适合 GitHub.io -->
  <script>
    (function() {
      // 获取所有区域
      const homeSection = document.getElementById('homeSection');
      const articlesSection = document.getElementById('articlesSection');
      const musicSection = document.getElementById('musicSection');
      const workSection = document.getElementById('workSection');
      const messagesSection = document.getElementById('messagesSection');

      // 所有菜单链接
      const menuLinks = document.querySelectorAll('.nav-item');
      const avatarHomeLink = document.getElementById('homeAvatarLink');

      // 隐藏所有内容区域
      function hideAllSections() {
        const sections = [homeSection, articlesSection, musicSection, workSection, messagesSection];
        sections.forEach(section => {
          if (section) {
            section.classList.add('hidden-section');
            section.classList.remove('active-section');
          }
        });
      }

      // 显示指定区域
      function showSection(sectionId) {
        hideAllSections();
        const target = document.getElementById(sectionId);
        if (target) {
          target.classList.remove('hidden-section');
          target.classList.add('active-section');
        }
      }

      // 移除所有菜单项的活跃样式（可选）
      function resetMenuActive() {
        menuLinks.forEach(link => {
          link.classList.remove('home-link-active');
        });
      }

      // 绑定菜单点击事件
      menuLinks.forEach(link => {
        link.addEventListener('click', function(e) {
          e.preventDefault();
          const sectionType = this.getAttribute('data-section');
          resetMenuActive();
          // 可根据需要高亮当前菜单项
          this.classList.add('home-link-active');

          switch (sectionType) {
            case 'articles':
              showSection('articlesSection');
              break;
            case 'music':
              showSection('musicSection');
              break;
            case 'work':
              showSection('workSection');
              break;
            case 'messages':
              showSection('messagesSection');
              break;
            default:
              // 默认回到主页
              showSection('homeSection');
              break;
          }
        });
      });

      // 头像点击返回主页 (同时移除菜单高亮)
      avatarHomeLink.addEventListener('click', function(e) {
        e.preventDefault();
        showSection('homeSection');
        resetMenuActive();
      });

      // 可选：如果点击了非菜单区域，但保留当前状态。
      // 初始化：保证主页可见 (默认已经通过html class实现)
      // 但如果某些浏览器缓存问题，手动确保
      window.addEventListener('load', function() {
        // 确保主页显示，其他隐藏
        hideAllSections();
        if (homeSection) {
          homeSection.classList.remove('hidden-section');
          homeSection.classList.add('active-section');
        }
        resetMenuActive();
      });

      // 处理浏览器可能的前进后退？简单处理，不做复杂路由。
    })();
  </script>
</body>
</html>
