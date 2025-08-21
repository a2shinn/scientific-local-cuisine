 index.html         
             <!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>郷土料理科学研究所 - 論文・統計・コメント機能付き</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Helvetica Neue', Arial, 'Hiragino Kaku Gothic ProN', 'Hiragino Sans', Meiryo, sans-serif;
            line-height: 1.6;
            color: #333;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }
        
        header {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            box-shadow: 0 2px 20px rgba(0, 0, 0, 0.1);
            position: fixed;
            width: 100%;
            top: 0;
            z-index: 1000;
            transition: all 0.3s ease;
        }
        
        nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 1rem 0;
        }
        
        .logo {
            font-size: 1.8rem;
            font-weight: bold;
            color: #4a5568;
            text-decoration: none;
        }
        
        .nav-links {
            display: flex;
            list-style: none;
            gap: 2rem;
            align-items: center;
        }
        
        .nav-links a {
            text-decoration: none;
            color: #4a5568;
            font-weight: 500;
            transition: color 0.3s ease;
            position: relative;
        }
        
        .nav-links a:hover {
            color: #667eea;
        }
        
        .admin-btn {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
            padding: 8px 16px;
            border-radius: 20px;
            text-decoration: none;
            font-size: 0.9rem;
            transition: all 0.3s ease;
        }
        
        .admin-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }
        
        main {
            margin-top: 80px;
            padding: 2rem 0;
        }
        
        .hero {
            text-align: center;
            padding: 4rem 0;
            color: white;
            margin-bottom: 3rem;
        }
        
        .hero h1 {
            font-size: 3.5rem;
            margin-bottom: 1rem;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
            animation: fadeInUp 1s ease;
        }
        
        .hero p {
            font-size: 1.3rem;
            margin-bottom: 2rem;
            opacity: 0.9;
            animation: fadeInUp 1s ease 0.2s both;
        }
        
        .hero-stats {
            display: flex;
            justify-content: center;
            gap: 3rem;
            margin-top: 2rem;
        }
        
        .hero-stat {
            text-align: center;
        }
        
        .hero-stat-number {
            font-size: 2.5rem;
            font-weight: bold;
            display: block;
        }
        
        .hero-stat-label {
            font-size: 1rem;
            opacity: 0.8;
        }
        
        /* 管理者ダッシュボード */
        .admin-panel {
            display: none;
            background: white;
            border-radius: 20px;
            padding: 2rem;
            margin: 2rem 0;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.1);
        }
        
        .admin-tabs {
            display: flex;
            gap: 1rem;
            margin-bottom: 2rem;
            border-bottom: 2px solid #e2e8f0;
            flex-wrap: wrap;
        }
        
        .admin-tab {
            padding: 10px 20px;
            background: none;
            border: none;
            color: #666;
            cursor: pointer;
            font-weight: 500;
            border-bottom: 2px solid transparent;
            transition: all 0.3s ease;
            white-space: nowrap;
        }
        
        .admin-tab.active {
            color: #667eea;
            border-bottom-color: #667eea;
        }
        
        .tab-content {
            display: none;
        }
        
        .tab-content.active {
            display: block;
        }
        
        /* 統計グリッド */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 1.5rem;
            margin-bottom: 2rem;
        }
        
        .stat-card {
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            color: white;
            padding: 1.5rem;
            border-radius: 15px;
            text-align: center;
            transition: transform 0.3s ease;
        }
        
        .stat-card:hover {
            transform: translateY(-5px);
        }
        
        .stat-number {
            font-size: 2rem;
            font-weight: bold;
            margin-bottom: 0.5rem;
        }
        
        /* 検索セクション */
        .search-section {
            background: white;
            border-radius: 20px;
            padding: 2rem;
            margin: 2rem 0;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.1);
        }
        
        .search-header {
            text-align: center;
            margin-bottom: 2rem;
        }
        
        .search-box-container {
            position: relative;
            max-width: 600px;
            margin: 0 auto 2rem;
        }
        
        .search-box {
            width: 100%;
            padding: 15px 20px 15px 50px;
            border: 2px solid #e2e8f0;
            border-radius: 50px;
            font-size: 1rem;
            outline: none;
            transition: all 0.3s ease;
        }
        
        .search-box:focus {
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
        }
        
        .search-icon {
            position: absolute;
            left: 15px;
            top: 50%;
            transform: translateY(-50%);
            color: #666;
            font-size: 1.2rem;
        }
        
        .filter-buttons {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 0.5rem;
        }
        
        .filter-btn {
            padding: 6px 16px;
            border: 2px solid #667eea;
            background: transparent;
            color: #667eea;
            border-radius: 25px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 0.9rem;
        }
        
        .filter-btn:hover,
        .filter-btn.active {
            background: #667eea;
            color: white;
        }
        
        /* 記事表示 */
        .articles-section {
            background: white;
            border-radius: 20px;
            padding: 3rem;
            margin: 2rem 0;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.1);
        }
        
        .section-header {
            text-align: center;
            margin-bottom: 3rem;
        }
        
        .section-title {
            font-size: 2.5rem;
            color: #4a5568;
            margin-bottom: 1rem;
        }
        
        .section-subtitle {
            font-size: 1.1rem;
            color: #666;
        }
        
        .articles-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(380px, 1fr));
            gap: 2rem;
        }
        
        .article-card {
            background: white;
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.1);
            transition: all 0.3s ease;
            cursor: pointer;
            position: relative;
        }
        
        .article-card:hover {
            transform: translateY(-8px);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.15);
        }
        
        .article-image {
            height: 220px;
            background: linear-gradient(45deg, #ffeaa7, #fab1a0);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 4rem;
            color: white;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
            position: relative;
        }
        
        .article-stats {
            position: absolute;
            top: 10px;
            right: 10px;
            background: rgba(255, 255, 255, 0.9);
            padding: 5px 10px;
            border-radius: 15px;
            font-size: 0.8rem;
            color: #666;
        }
        
        .article-rating {
            position: absolute;
            top: 10px;
            left: 10px;
            background: rgba(255, 255, 255, 0.9);
            padding: 5px 10px;
            border-radius: 15px;
            font-size: 0.8rem;
            color: #ff6b6b;
            font-weight: bold;
        }
        
        .article-content {
            padding: 1.5rem;
        }
        
        .article-meta {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1rem;
            font-size: 0.9rem;
            color: #666;
        }
        
        .article-category {
            background: #667eea;
            color: white;
            padding: 3px 10px;
            border-radius: 15px;
            font-size: 0.8rem;
        }
        
        .article-title {
            font-size: 1.3rem;
            font-weight: bold;
            color: #4a5568;
            margin-bottom: 0.8rem;
        }
        
        .article-description {
            color: #666;
            margin-bottom: 1rem;
            line-height: 1.5;
        }
        
        .article-research {
            background: #f8f9ff;
            padding: 1rem;
            border-radius: 10px;
            border-left: 4px solid #667eea;
            margin: 1rem 0;
        }
        
        .research-title {
            font-weight: bold;
            font-size: 0.9rem;
            color: #4a5568;
            margin-bottom: 0.5rem;
        }
        
        .research-citation {
            font-size: 0.8rem;
            color: #666;
            font-style: italic;
        }
        
        .article-footer {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-top: 1rem;
            padding-top: 1rem;
            border-top: 1px solid #e2e8f0;
        }
        
        .article-actions {
            display: flex;
            gap: 0.5rem;
        }
        
        .action-btn {
            padding: 5px 12px;
            border: 1px solid #e2e8f0;
            background: white;
            border-radius: 20px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 0.8rem;
        }
        
        .action-btn:hover {
            background: #f8f9ff;
            border-color: #667eea;
        }
        
        .comments-count {
            color: #666;
            font-size: 0.9rem;
        }
        
        /* フォーム */
        .form-group {
            margin-bottom: 1.5rem;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: bold;
            color: #4a5568;
        }
        
        .form-group input,
        .form-group textarea,
        .form-group select {
            width: 100%;
            padding: 12px;
            border: 2px solid #e2e8f0;
            border-radius: 8px;
            font-size: 1rem;
            transition: border-color 0.3s ease;
        }
        
        .form-group input:focus,
        .form-group textarea:focus,
        .form-group select:focus {
            outline: none;
            border-color: #667eea;
        }
        
        .form-group textarea {
            min-height: 120px;
            resize: vertical;
        }
        
        .btn {
            padding: 12px 24px;
            border: none;
            border-radius: 8px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            margin-right: 1rem;
        }
        
        .btn-primary {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
        }
        
        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }
        
        /* レスポンシブ */
        @media (max-width: 768px) {
            .hero h1 {
                font-size: 2.5rem;
            }
            
            .hero-stats {
                flex-direction: column;
                gap: 1rem;
            }
            
            .nav-links {
                flex-direction: column;
                gap: 1rem;
            }
            
            .admin-tabs {
                flex-direction: column;
            }
            
            .articles-grid {
                grid-template-columns: 1fr;
            }
        }
        
        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        /* 特別バッジ */
        .research-badge {
            background: linear-gradient(45deg, #11998e, #38ef7d);
            color: white;
            padding: 3px 8px;
            border-radius: 12px;
            font-size: 0.7rem;
            font-weight: bold;
            margin-left: 0.5rem;
        }
    </style>
</head>
<body>
    <header>
        <nav class="container">
            <a href="#" class="logo">🧬 郷土料理科学研究所</a>
            <ul class="nav-links">
                <li><a href="#home">ホーム</a></li>
                <li><a href="#articles">論文・記事</a></li>
                <li><a href="#search">検索</a></li>
                <li><a href="#" class="admin-btn" onclick="toggleAdminPanel()">📊 管理画面</a></li>
            </ul>
        </nav>
    </header>

    <main class="container">
        <section id="home" class="hero">
            <h1>🔬 郷土料理科学研究所</h1>
            <p>論文・統計データに基づく科学的郷土料理研究プラットフォーム</p>
            <div class="hero-stats">
                <div class="hero-stat">
                    <span class="hero-stat-number" id="heroViews">1</span>
                    <span class="hero-stat-label">総研究閲覧数</span>
                </div>
                <div class="hero-stat">
                    <span class="hero-stat-number" id="heroPapers">0</span>
                    <span class="hero-stat-label">引用論文数</span>
                </div>
                <div class="hero-stat">
                    <span class="hero-stat-number" id="heroComments">0</span>
                    <span class="hero-stat-label">コメント数</span>
                </div>
            </div>
        </section>

        <!-- 管理者パネル -->
        <section class="admin-panel" id="adminPanel">
            <div class="admin-tabs">
                <button class="admin-tab active" onclick="switchTab('create')">✏️ 記事投稿</button>
                <button class="admin-tab" onclick="switchTab('analytics')">📊 分析</button>
                <button class="admin-tab" onclick="switchTab('manage')">📝 管理</button>
            </div>

            <!-- 記事投稿タブ -->
            <div id="create-tab" class="tab-content active">
                <h3>✏️ 新しい研究記事を投稿</h3>
                <form id="articleForm">
                    <div class="form-group">
                        <label for="title">記事タイトル</label>
                        <input type="text" id="title" name="title" placeholder="例：味噌の発酵過程における機能性成分の変化">
                    </div>
                    
                    <div class="form-group">
                        <label for="region">対象地域</label>
                        <select id="region" name="region">
                            <option value="全国">全国</option>
                            <option value="北海道">北海道</option>
                            <option value="東北">東北</option>
                            <option value="関東">関東</option>
                            <option value="中部">中部</option>
                            <option value="関西">関西</option>
                            <option value="中国">中国</option>
                            <option value="四国">四国</option>
                            <option value="九州">九州</option>
                        </select>
                    </div>
                    
                    <div class="form-group">
                        <label for="emoji">料理アイコン</label>
                        <input type="text" id="emoji" name="emoji" placeholder="🍲" maxlength="2">
                    </div>
                    
                    <div class="form-group">
                        <label for="description">研究概要</label>
                        <textarea id="description" name="description" placeholder="この研究の目的、方法、主要な発見について簡潔に説明してください..."></textarea>
                    </div>
                    
                    <div class="form-group">
                        <label for="findings">主要な発見</label>
                        <textarea id="findings" name="findings" placeholder="研究で得られた主要な結果、科学的知見について説明してください..."></textarea>
                    </div>
                    
                    <div class="form-group">
                        <label for="nutrition">栄養・成分データ</label>
                        <textarea id="nutrition" name="nutrition" placeholder="例：タンパク質: 18.5g/100g, ビタミンB1: 0.8mg/100g"></textarea>
                    </div>
                    
                    <button type="submit" class="btn btn-primary">📝 研究記事を投稿</button>
                </form>
            </div>

            <!-- 分析タブ -->
            <div id="analytics-tab" class="tab-content">
                <h3>📈 サイト統計</h3>
                <div class="stats-grid">
                    <div class="stat-card">
                        <div class="stat-number" id="totalUsers">1</div>
                        <div>総ユーザー数</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-number" id="dailyUsers">1</div>
                        <div>本日の訪問者</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-number" id="totalArticles">0</div>
                        <div>投稿記事数</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-number" id="avgTime">0:00</div>
                        <div>平均滞在時間</div>
                    </div>
                </div>
                <p style="text-align: center; color: #666; margin-top: 2rem;">
                    📝 記事を投稿すると統計データが蓄積されます
                </p>
            </div>

            <!-- 管理タブ -->
            <div id="manage-tab" class="tab-content">
                <h3>📝 記事管理</h3>
                <div id="articleList">
                    <p style="text-align: center; color: #666; margin: 2rem 0;">
                        まだ記事が投稿されていません。<br>
                        「✏️ 記事投稿」タブから最初の記事を投稿してみましょう！
                    </p>
                </div>
            </div>
        </section>

        <!-- 検索セクション -->
        <section id="search" class="search-section">
            <div class="search-header">
                <h2>🔍 研究検索</h2>
                <p>論文、栄養成分、研究手法、地域などで検索</p>
            </div>
            
            <div class="search-box-container">
                <div class="search-icon">🔍</div>
                <input type="text" class="search-box" placeholder="研究内容、栄養成分、キーワードで検索..." id="searchInput">
            </div>
            
            <div class="filter-buttons">
                <button class="filter-btn active" data-filter="all">すべて</button>
                <button class="filter-btn" data-filter="東北">東北</button>
                <button class="filter-btn" data-filter="関東">関東</button>
                <button class="filter-btn" data-filter="中部">中部</button>
                <button class="filter-btn" data-filter="関西">関西</button>
                <button class="filter-btn" data-filter="九州">九州</button>
            </div>
        </section>

        <!-- 記事一覧セクション -->
        <section id="articles" class="articles-section">
            <div class="section-header">
                <h2 class="section-title">📚 研究記事</h2>
                <p class="section-subtitle">科学的根拠に基づく郷土料理研究</p>
            </div>
            
            <div class="articles-grid" id="articlesGrid">
                <div style="text-align: center; color: #666; padding: 3rem; grid-column: 1/-1;">
                    <h3>📝 最初の記事を投稿してみましょう！</h3>
                    <p>管理画面の「✏️ 記事投稿」から研究記事を追加できます</p>
                    <button class="btn btn-primary" onclick="toggleAdminPanel()" style="margin-top: 1rem;">
                        📊 管理画面を開く
                    </button>
                </div>
            </div>
        </section>
    </main>

    <footer style="background: rgba(0, 0, 0, 0.8); color: white; text-align: center; padding: 2rem 0; margin-top: 3rem;">
        <div class="container">
            <p>&copy; 2025 郷土料理科学研究所 - あなたの研究成果を世界に発信</p>
            <p>🧪 科学的根拠に基づいた郷土料理研究プラットフォーム</p>
        </div>
    </footer>

    <script>
        // 管理者パネルの表示切替
        function toggleAdminPanel() {
            const panel = document.getElementById('adminPanel');
            panel.style.display = panel.style.display === 'none' ? 'block' : 
                                 panel.style.display === 'block' ? 'none' : 'block';
        }

        // タブの切り替え
        function switchTab(tabName) {
            const tabs = document.querySelectorAll('.tab-content');
            tabs.forEach(tab => tab.classList.remove('active'));
            
            const buttons = document.querySelectorAll('.admin-tab');
            buttons.forEach(btn => btn.classList.remove('active'));
            
            document.getElementById(tabName + '-tab').classList.add('active');
            event.target.classList.add('active');
        }

        // 記事投稿フォーム処理
        document.getElementById('articleForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const formData = new FormData(this);
            const articleData = {
                title: formData.get('title'),
                region: formData.get('region'),
                emoji: formData.get('emoji'),
                description: formData.get('description'),
                findings: formData.get('findings'),
                nutrition: formData.get('nutrition'),
                views: 1,
                comments: 0,
                rating: 5.0,
                dateCreated: new Date().toLocaleDateString('ja-JP')
            };
            
            if (articleData.title && articleData.description) {
                addNewArticleCard(articleData);
                
                // 統計更新
                document.getElementById('heroPapers').textContent = 
                    parseInt(document.getElementById('heroPapers').textContent) + 1;
                document.getElementById('totalArticles').textContent = 
                    parseInt(document.getElementById('totalArticles').textContent) + 1;
                
                alert('📝 研究記事が正常に投稿されました！');
                clearForm();
            } else {
                alert('タイトルと研究概要は必須です。');
            }
        });

        // 新しい記事カードを追加
        function addNewArticleCard(data) {
            const articlesGrid = document.getElementById('articlesGrid');
            
            // 初期メッセージを削除
            const placeholder = articlesGrid.querySelector('div[style*="grid-column"]');
            if (placeholder) {
                placeholder.remove();
            }
            
            const newCard = document.createElement('div');
            newCard.className = 'article-card';
            
            newCard.innerHTML = `
                <div class="article-image">${data.emoji || '📄'}
                    <div class="article-rating">⭐ ${data.rating}</div>
                    <div class="article-stats">👁️ ${data.views} 💬 ${data.comments}</div>
                </div>
                <div class="article-content">
                    <div class="article-meta">
                        <span class="article-category">研究記事</span>
                        <span>${data.dateCreated}</span>
                    </div>
                    <h3 class="article-title">${data.title}<span class="research-badge">新着</span></h3>
                    <p class="article-description">${data.description}</p>
                    <div class="article-research">
                        <div class="research-title">🔬 主要な科学的知見</div>
                        <p>${data.findings}</p>
                    </div>
                    <div class="article-footer">
                        <div class="article-actions">
                            <button class="action-btn">❤️ お気に入り</button>
                            <button class="action-btn">📤 シェア</button>
                        </div>
                        <div class="comments-count">💬 ${data.comments}件のコメント</div>
                    </div>
                </div>
            `;
            
            articlesGrid.appendChild(newCard);
        }

        // フォームクリア
        function clearForm() {
            document.getElementById('articleForm').reset();
        }

        // 統計の更新（訪問者数カウント）
        function updateStats() {
            const currentViews = parseInt(document.getElementById('heroViews').textContent);
            document.getElementById('heroViews').textContent = currentViews + 1;
        }

        // ページ読み込み時に統計更新
        window.addEventListener('load', function() {
            updateStats();
        });

        // スムーズスクロール
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();
                const target = document.querySelector(this.getAttribute('href'));
                if (target) {
                    target.scrollIntoView({
                        behavior: 'smooth',
                        block: 'start'
                    });
                }
            });
        });
    </script>
</body>
</html>             
