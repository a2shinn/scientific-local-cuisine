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
        
        /* 読者分析 */
        .analytics-section {
            background: #f8f9ff;
            padding: 1.5rem;
            border-radius: 15px;
            margin: 1rem 0;
        }
        
        .reader-demographics {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 1.5rem;
        }
        
        .demographic-chart {
            background: white;
            padding: 1rem;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }
        
        .chart-title {
            font-weight: bold;
            margin-bottom: 1rem;
            color: #4a5568;
        }
        
        .chart-bar {
            display: flex;
            align-items: center;
            margin-bottom: 0.8rem;
        }
        
        .chart-label {
            width: 100px;
            font-size: 0.9rem;
        }
        
        .chart-progress {
            flex: 1;
            height: 20px;
            background: #e2e8f0;
            border-radius: 10px;
            margin: 0 1rem;
            overflow: hidden;
        }
        
        .chart-fill {
            height: 100%;
            background: linear-gradient(45deg, #667eea, #764ba2);
            transition: width 0.5s ease;
        }
        
        .chart-value {
            font-weight: bold;
            font-size: 0.9rem;
            color: #667eea;
        }
        
        /* フォームスタイル */
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
        
        .form-row {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 1rem;
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
        
        .btn-secondary {
            background: #e2e8f0;
            color: #4a5568;
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
        
        .advanced-search {
            background: #f8f9ff;
            padding: 1.5rem;
            border-radius: 15px;
            margin-top: 1rem;
        }
        
        .filter-section {
            margin-bottom: 1.5rem;
        }
        
        .filter-title {
            font-weight: bold;
            margin-bottom: 0.8rem;
            color: #4a5568;
        }
        
        .filter-buttons {
            display: flex;
            flex-wrap: wrap;
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
        
        /* モーダル */
        .modal {
            display: none;
            position: fixed;
            z-index: 2000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.8);
            backdrop-filter: blur(5px);
        }
        
        .modal-content {
            background-color: white;
            margin: 2% auto;
            padding: 0;
            border-radius: 20px;
            width: 90%;
            max-width: 800px;
            max-height: 90vh;
            overflow-y: auto;
            position: relative;
            animation: modalFadeIn 0.3s ease;
        }
        
        .modal-header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 2rem;
            border-radius: 20px 20px 0 0;
        }
        
        .modal-body {
            padding: 2rem;
        }
        
        .close {
            position: absolute;
            right: 1rem;
            top: 1rem;
            font-size: 2rem;
            cursor: pointer;
            color: white;
            transition: color 0.3s ease;
        }
        
        .close:hover {
            color: #ddd;
        }
        
        /* コメントセクション */
        .comments-section {
            margin-top: 2rem;
            padding-top: 2rem;
            border-top: 2px solid #e2e8f0;
        }
        
        .comment-form {
            background: #f8f9ff;
            padding: 1.5rem;
            border-radius: 15px;
            margin-bottom: 2rem;
        }
        
        .comment-form h4 {
            margin-bottom: 1rem;
            color: #4a5568;
        }
        
        .comment-input {
            width: 100%;
            min-height: 100px;
            padding: 12px;
            border: 2px solid #e2e8f0;
            border-radius: 8px;
            resize: vertical;
            margin-bottom: 1rem;
        }
        
        .comment-input:focus {
            outline: none;
            border-color: #667eea;
        }
        
        .comments-list {
            space: 1rem;
        }
        
        .comment {
            background: #f9f9f9;
            padding: 1rem;
            border-radius: 10px;
            margin-bottom: 1rem;
            border-left: 4px solid #667eea;
        }
        
        .comment-header {
            display: flex;
            justify-content: space-between;
            margin-bottom: 0.5rem;
        }
        
        .comment-author {
            font-weight: bold;
            color: #4a5568;
        }
        
        .comment-date {
            color: #666;
            font-size: 0.9rem;
        }
        
        .comment-text {
            color: #555;
            line-height: 1.5;
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
            
            .form-row {
                grid-template-columns: 1fr;
            }
            
            .reader-demographics {
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
        
        @keyframes modalFadeIn {
            from {
                opacity: 0;
                transform: scale(0.7);
            }
            to {
                opacity: 1;
                transform: scale(1);
            }
        }
        
        /* スペシャルタグ */
        .research-badge {
            background: linear-gradient(45deg, #11998e, #38ef7d);
            color: white;
            padding: 3px 8px;
            border-radius: 12px;
            font-size: 0.7rem;
            font-weight: bold;
            margin-left: 0.5rem;
        }
        
        .trending-badge {
            background: linear-gradient(45deg, #ff6b6b, #ee5a24);
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
                    <span class="hero-stat-number" id="heroViews">24,891</span>
                    <span class="hero-stat-label">総研究閲覧数</span>
                </div>
                <div class="hero-stat">
                    <span class="hero-stat-number" id="heroPapers">127</span>
                    <span class="hero-stat-label">引用論文数</span>
                </div>
                <div class="hero-stat">
                    <span class="hero-stat-number" id="heroComments">1,847</span>
                    <span class="hero-stat-label">コメント数</span>
                </div>
            </div>
        </section>

        <!-- 管理者パネル -->
        <section class="admin-panel" id="adminPanel">
            <div class="admin-tabs">
                <button class="admin-tab active" onclick="switchTab('analytics')">📊 詳細分析</button>
                <button class="admin-tab" onclick="switchTab('demographics')">👥 読者分析</button>
                <button class="admin-tab" onclick="switchTab('create')">✏️ 記事投稿</button>
                <button class="admin-tab" onclick="switchTab('manage')">📝 記事管理</button>
                <button class="admin-tab" onclick="switchTab('comments')">💬 コメント管理</button>
            </div>

            <!-- 詳細分析タブ -->
            <div id="analytics-tab" class="tab-content active">
                <h3>📈 サイト詳細統計</h3>
                <div class="stats-grid">
                    <div class="stat-card">
                        <div class="stat-number" id="totalUsers">8,234</div>
                        <div>総ユーザー数</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-number" id="dailyUsers">342</div>
                        <div>日間アクティブユーザー</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-number" id="avgTime">5:42</div>
                        <div>平均滞在時間</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-number" id="bounceRate">23%</div>
                        <div>直帰率</div>
                    </div>
                </div>

                <div class="analytics-section">
                    <h4>🔥 人気研究記事ランキング</h4>
                    <div class="chart-title">過去30日間のアクセス数</div>
                    <div class="chart-bar">
                        <div class="chart-label">発酵の科学</div>
                        <div class="chart-progress">
                            <div class="chart-fill" style="width: 95%"></div>
                        </div>
                        <div class="chart-value">2,847</div>
                    </div>
                    <div class="chart-bar">
                        <div class="chart-label">栄養分析</div>
                        <div class="chart-progress">
                            <div class="chart-fill" style="width: 78%"></div>
                        </div>
                        <div class="chart-value">2,231</div>
                    </div>
                    <div class="chart-bar">
                        <div class="chart-label">調理化学</div>
                        <div class="chart-progress">
                            <div class="chart-fill" style="width: 65%"></div>
                        </div>
                        <div class="chart-value">1,875</div>
                    </div>
                    <div class="chart-bar">
                        <div class="chart-label">地域比較</div>
                        <div class="chart-progress">
                            <div class="chart-fill" style="width: 52%"></div>
                        </div>
                        <div class="chart-value">1,492</div>
                    </div>
                </div>

                <div class="analytics-section">
                    <h4>🔍 人気検索キーワード</h4>
                    <div class="filter-buttons">
                        <span class="filter-btn active">発酵</span>
                        <span class="filter-btn active">栄養成分</span>
                        <span class="filter-btn active">タンパク質</span>
                        <span class="filter-btn active">ビタミン</span>
                        <span class="filter-btn">アミノ酸</span>
                        <span class="filter-btn">抗酸化</span>
                        <span class="filter-btn">機能性</span>
                        <span class="filter-btn">地域特産</span>
                    </div>
                </div>
            </div>

            <!-- 読者分析タブ -->
            <div id="demographics-tab" class="tab-content">
                <h3>👥 読者層詳細分析</h3>
                <div class="reader-demographics">
                    <div class="demographic-chart">
                        <div class="chart-title">📊 年齢層分布</div>
                        <div class="chart-bar">
                            <div class="chart-label">18-29歳</div>
                            <div class="chart-progress">
                                <div class="chart-fill" style="width: 35%"></div>
                            </div>
                            <div class="chart-value">35%</div>
                        </div>
                        <div class="chart-bar">
                            <div class="chart-label">30-39歳</div>
                            <div class="chart-progress">
                                <div class="chart-fill" style="width: 28%"></div>
                            </div>
                            <div class="chart-value">28%</div>
                        </div>
                        <div class="chart-bar">
                            <div class="chart-label">40-49歳</div>
                            <div class="chart-progress">
                                <div class="chart-fill" style="width: 22%"></div>
                            </div>
                            <div class="chart-value">22%</div>
                        </div>
                        <div class="chart-bar">
                            <div class="chart-label">50歳以上</div>
                            <div class="chart-progress">
                                <div class="chart-fill" style="width: 15%"></div>
                            </div>
                            <div class="chart-value">15%</div>
                        </div>
                    </div>

                    <div class="demographic-chart">
                        <div class="chart-title">🎓 職業・専門分野</div>
                        <div class="chart-bar">
                            <div class="chart-label">研究者</div>
                            <div class="chart-progress">
                                <div class="chart-fill" style="width: 32%"></div>
                            </div>
                            <div class="chart-value">32%</div>
                        </div>
                        <div class="chart-bar">
                            <div class="chart-label">栄養士</div>
                            <div class="chart-progress">
                                <div class="chart-fill" style="width: 24%"></div>
                            </div>
                            <div class="chart-value">24%</div>
                        </div>
                        <div class="chart-bar">
                            <div class="chart-label">料理関係者</div>
                            <div class="chart-progress">
                                <div class="chart-fill" style="width: 18%"></div>
                            </div>
                            <div class="chart-value">18%</div>
                        </div>
                        <div class="chart-bar">
                            <div class="chart-label">学生</div>
                            <div class="chart-progress">
                                <div class="chart-fill" style="width: 16%"></div>
                            </div>
                            <div class="chart-value">16%</div>
                        </div>
                        <div class="chart-bar">
                            <div class="chart-label">その他</div>
                            <div class="chart-progress">
                                <div class="chart-fill" style="width: 10%"></div>
                            </div>
                            <div class="chart-value">10%</div>
                        </div>
                    </div>

                    <div class="demographic-chart">
                        <div class="chart-title">📍 地域分布</div>
                        <div class="chart-bar">
                            <div class="chart-label">関東</div>
                            <div class="chart-progress">
                                <div class="chart-fill" style="width: 38%"></div>
                            </div>
                            <div class="chart-value">38%</div>
                        </div>
                        <div class="chart-bar">
                            <div class="chart-label">関西</div>
                            <div class="chart-progress">
                                <div class="chart-fill" style="width: 22%"></div>
                            </div>
                            <div class="chart-value">22%</div>
                        </div>
                        <div class="chart-bar">
                            <div class="chart-label">中部</div>
                            <div class="chart-progress">
                                <div class="chart-fill" style="width: 15%"></div>
                            </div>
                            <div class="chart-value">15%</div>
                        </div>
                        <div class="chart-bar">
                            <div class="chart-label">その他</div>
                            <div class="chart-progress">
                                <div class="chart-fill" style="width: 25%"></div>
                            </div>
                            <div class="chart-value">25%</div>
                        </div>
                    </div>

                    <div class="demographic-chart">
                        <div class="chart-title">📚 関心分野</div>
                        <div class="chart-bar">
                            <div class="chart-label">栄養学</div>
                            <div class="chart-progress">
                                <div class="chart-fill" style="width: 45%"></div>
                            </div>
                            <div class="chart-value">45%</div>
                        </div>
                        <div class="chart-bar">
                            <div class="chart-label">食品科学</div>
                            <div class="chart-progress">
                                <div class="chart-fill" style="width: 38%"></div>
                            </div>
                            <div class="chart-value">38%</div>
                        </div>
                        <div class="chart-bar">
                            <div class="chart-label">文化研究</div>
                            <div class="chart-progress">
                                <div class="chart-fill" style="width: 28%"></div>
                            </div>
                            <div class="chart-value">28%</div>
                        </div>
                        <div class="chart-bar">
                            <div class="chart-label">調理技術</div>
                            <div class="chart-progress">
                                <div class="chart-fill" style="width: 22%"></div>
                            </div>
                            <div class="chart-value">22%</div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- 記事投稿タブ -->
            <div id="create-tab" class="tab-content">
                <h3>✏️ 新しい研究記事を投稿</h3>
                <form id="articleForm">
                    <div class="form-row">
                        <div class="form-group">
                            <label for="title">記事タイトル</label>
                            <input type="text" id="title" name="title" placeholder="例：味噌の発酵過程における機能性成分の変化">
                        </div>
                        <div class="form-group">
                            <label for="category">カテゴリー</label>
                            <select id="category" name="category">
                                <option value="発酵食品">発酵食品</option>
                                <option value="栄養分析">栄養分析</option>
                                <option value="調理科学">調理科学</option>
                                <option value="地域比較">地域比較</option>
                                <option value="機能性成分">機能性成分</option>
                                <option value="食品安全">食品安全</option>
                            </select>
                        </div>
                    </div>
                    
                    <div class="form-row">
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
                    </div>
                    
                    <div class="form-group">
                        <label for="description">研究概要</label>
                        <textarea id="description" name="description" placeholder="この研究の目的、方法、主要な発見について簡潔に説明してください..."></textarea>
                    </div>
                    
                    <div class="form-group">
                        <label for="methodology">研究方法</label>
                        <textarea id="methodology" name="methodology" placeholder="実験方法、分析手法、サンプリング方法などについて詳しく説明してください..."></textarea>
                    </div>
                    
                    <div class="form-group">
                        <label for="findings">主要な発見</label>
                        <textarea id="findings" name="findings" placeholder="研究で得られた主要な結果、科学的知見について説明してください..."></textarea>
                    </div>
                    
                    <div class="form-group">
                        <label for="nutrition">栄養・成分データ</label>
                        <textarea id="nutrition" name="nutrition" placeholder="例：タンパク質: 18.5g/100g, ビタミンB1: 0.8mg/100g, 抗酸化活性: DPPH IC50 = 45.2μg/ml"></textarea>
                    </div>
                    
                    <div class="form-group">
                        <label for="citations">参考文献・引用</label>
                        <textarea id="citations" name="citations" placeholder="例：田中太郎 et al. (2023). 発酵食品の機能性成分に関する研究. 日本食品科学会誌, 45(3), 123-135."></textarea>
                    </div>
                    
                    <button type="submit" class="btn btn-primary">📝 研究記事を投稿</button>
                    <button type="button" class="btn btn-secondary" onclick="clearForm()">🗑️ クリア</button>
                </form>
            </div>

            <!-- 記事管理タブ -->
            <div id="manage-tab" class="tab-content">
                <h3>📝 記事管理</h3>
                <div id="articleList">
                    <div class="article-item" style="border: 1px solid #e2e8f0; padding: 1rem; margin: 1rem 0; border-radius: 8px;">
                        <h4>発酵食品の機能性成分分析 <span style="color: #667eea;">(閲覧数: 2,847, コメント: 23)</span></h4>
                        <p>カテゴリー: 発酵食品 | 地域: 全国 | 投稿日: 2025-01-15</p>
                        <button class="btn btn-primary" onclick="editArticle('fermentation-analysis')">✏️ 編集</button>
                        <button class="btn btn-secondary" onclick="deleteArticle('fermentation-analysis')">🗑️ 削除</button>
                    </div>
                    <div class="article-item" style="border: 1px solid #e2e8f0; padding: 1rem; margin: 1rem 0; border-radius: 8px;">
                        <h4>地域別栄養価比較研究 <span style="color: #667eea;">(閲覧数: 1,875, コメント: 15)</span></h4>
                        <p>カテゴリー: 栄養分析 | 地域: 東北 | 投稿日: 2025-01-10</p>
                        <button class="btn btn-primary" onclick="editArticle('nutrition-comparison')">✏️ 編集</button>
                        <button class="btn btn-secondary" onclick="deleteArticle('nutrition-comparison')">🗑️ 削除</button>
                    </div>
                </div>
            </div>

            <!-- コメント管理タブ -->
            <div id="comments-tab" class="tab-content">
                <h3>💬 コメント管理</h3>
                <div class="analytics-section">
                    <h4>📊 コメント統計</h4>
                    <div class="stats-grid">
                        <div class="stat-card">
                            <div class="stat-number">1,847</div>
                            <div>総コメント数</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-number">124</div>
                            <div>今月のコメント</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-number">8.7</div>
                            <div>記事あたり平均コメント数</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-number">92%</div>
                            <div>コメント承認率</div>
                        </div>
                    </div>
                </div>
                
                <div class="analytics-section">
                    <h4>⏰ 最新コメント</h4>
                    <div class="comment">
                        <div class="comment-header">
                            <div class="comment-author">田中研究員</div>
                            <div class="comment-date">2時間前</div>
                        </div>
                        <div class="comment-text">発酵過程でのビタミンB12の増加について、追加の検証実験データはありますか？非常に興味深い研究です。</div>
                    </div>
                    <div class="comment">
                        <div class="comment-header">
                            <div class="comment-author">栄養士_佐藤</div>
                            <div class="comment-date">5時間前</div>
                        </div>
                        <div class="comment-text">地域差による栄養価の違いが明確に示されていて、臨床現場でも活用できそうです。素晴らしい研究ですね。</div>
                    </div>
                </div>
            </div>
        </section>

        <!-- 検索セクション -->
        <section id="search" class="search-section">
            <div class="search-header">
                <h2>🔍 高度な研究検索</h2>
                <p>論文、栄養成分、研究手法、地域などで詳細検索</p>
            </div>
            
            <div class="search-box-container">
                <div class="search-icon">🔍</div>
                <input type="text" class="search-box" placeholder="研究内容、栄養成分、論文著者、キーワードで検索..." id="searchInput">
            </div>
            
            <div class="advanced-search">
                <div class="filter-section">
                    <div class="filter-title">🧪 研究分野</div>
                    <div class="filter-buttons">
                        <button class="filter-btn active" data-filter="all">すべて</button>
                        <button class="filter-btn" data-filter="発酵食品">発酵食品</button>
                        <button class="filter-btn" data-filter="栄養分析">栄養分析</button>
                        <button class="filter-btn" data-filter="調理科学">調理科学</button>
                        <button class="filter-btn" data-filter="機能性成分">機能性成分</button>
                        <button class="filter-btn" data-filter="地域比較">地域比較</button>
                    </div>
                </div>
                
                <div class="filter-section">
                    <div class="filter-title">📍 対象地域</div>
                    <div class="filter-buttons">
                        <button class="filter-btn active" data-region="all">全地域</button>
                        <button class="filter-btn" data-region="東北">東北</button>
                        <button class="filter-btn" data-region="関東">関東</button>
                        <button class="filter-btn" data-region="中部">中部</button>
                        <button class="filter-btn" data-region="関西">関西</button>
                        <button class="filter-btn" data-region="九州">九州</button>
                    </div>
                </div>
                
                <div class="filter-section">
                    <div class="filter-title">⭐ 評価・人気度</div>
                    <div class="filter-buttons">
                        <button class="filter-btn" data-rating="all">すべて</button>
                        <button class="filter-btn" data-rating="high">高評価(4.0以上)</button>
                        <button class="filter-btn" data-rating="popular">人気記事</button>
                        <button class="filter-btn" data-rating="recent">最新研究</button>
                    </div>
                </div>
            </div>
        </section>

        <!-- 記事一覧セクション -->
        <section id="articles" class="articles-section">
            <div class="section-header">
                <h2 class="section-title">📚 最新研究記事</h2>
                <p class="section-subtitle">科学的根拠に基づく郷土料理研究の最前線</p>
            </div>
            
            <div class="articles-grid" id="articlesGrid">
                <div class="article-card" data-category="発酵食品" data-region="秋田県" data-rating="4.8">
                    <div class="article-image">🍲
                        <div class="article-rating">⭐ 4.8</div>
                        <div class="article-stats">👁️ 2,847 💬 23</div>
                    </div>
                    <div class="article-content">
                        <div class="article-meta">
                            <span class="article-category">発酵食品</span>
                            <span>2025-01-15</span>
                        </div>
                        <h3 class="article-title">きりたんぽの発酵過程における機能性成分の変化<span class="research-badge">査読済</span></h3>
                        <p class="article-description">秋田県のきりたんぽ製造過程で生成される機能性ペプチドと乳酸菌の相互作用について、最新の分析技術を用いて詳細に調査しました。</p>
                        <div class="article-research">
                            <div class="research-title">🔬 主要な科学的知見</div>
                            <p>比内地鶏由来のタンパク質が発酵過程で機能性ペプチドに変換され、ACE阻害活性が48%向上することを確認。</p>
                            <div class="research-citation">出典: 田中太郎 et al. (2025). 日本発酵学会誌, 48(2), 89-102.</div>
                        </div>
                        <div class="article-footer">
                            <div class="article-actions">
                                <button class="action-btn" onclick="toggleFavorite(this)">❤️ お気に入り</button>
                                <button class="action-btn" onclick="shareArticle(this)">📤 シェア</button>
                            </div>
                            <div class="comments-count">💬 23件のコメント</div>
                        </div>
                    </div>
                </div>

                <div class="article-card" data-category="栄養分析" data-region="福岡県" data-rating="4.6">
                    <div class="article-image">🌶️
                        <div class="article-rating">⭐ 4.6</div>
                        <div class="article-stats">👁️ 2,231 💬 18</div>
                    </div>
                    <div class="article-content">
                        <div class="article-meta">
                            <span class="article-category">栄養分析</span>
                            <span>2025-01-12</span>
                        </div>
                        <h3 class="article-title">明太子の抗酸化成分と健康機能性の包括的分析<span class="trending-badge">トレンド</span></h3>
                        <p class="article-description">福岡県産明太子に含まれるカプサイシンとアスタキサンチンの抗酸化活性について、HPLC-MS/MSを用いた定量分析を実施。</p>
                        <div class="article-research">
                            <div class="research-title">🔬 主要な科学的知見</div>
                            <p>明太子のDPPH ラジカル消去活性はIC50=23.4μg/mlで、同重量のブルーベリーより高い抗酸化力を示した。</p>
                            <div class="research-citation">出典: 佐藤花子 et al. (2025). 食品科学工学会誌, 72(1), 45-58.</div>
                        </div>
                        <div class="article-footer">
                            <div class="article-actions">
                                <button class="action-btn" onclick="toggleFavorite(this)">❤️ お気に入り</button>
                                <button class="action-btn" onclick="shareArticle(this)">📤 シェア</button>
                            </div>
                            <div class="comments-count">💬 18件のコメント</div>
                        </div>
                    </div>
                </div>

                <div class="article-card" data-category="調理科学" data-region="香川県" data-rating="4.5">
                    <div class="article-image">🍜
                        <div class="article-rating">⭐ 4.5</div>
                        <div class="article-stats">👁️ 1,875 💬 15</div>
                    </div>
                    <div class="article-content">
                        <div class="article-meta">
                            <span class="article-category">調理科学</span>
                            <span>2025-01-10</span>
                        </div>
                        <h3 class="article-title">讃岐うどんのグルテン構造と食感の分子レベル解析</h3>
                        <p class="article-description">讃岐うどん特有のコシの秘密を、小麦粉のグルテン分子構造とタンパク質の三次元配列から科学的に解明しました。</p>
                        <div class="article-research">
                            <div class="research-title">🔬 主要な科学的知見</div>
                            <p>香川県産小麦粉のグルテニン/グリアジン比が1.8:1で、これが独特の弾力性を生み出す要因であることを特定。</p>
                            <div class="research-citation">出典: 山田次郎 et al. (2025). 日本調理科学会誌, 58(1), 12-25.</div>
                        </div>
                        <div class="article-footer">
                            <div class="article-actions">
                                <button class="action-btn" onclick="toggleFavorite(this)">❤️ お気に入り</button>
                                <button class="action-btn" onclick="shareArticle(this)">📤 シェア</button>
                            </div>
                            <div class="comments-count">💬 15件のコメント</div>
                        </div>
                    </div>
                </div>

                <div class="article-card" data-category="機能性成分" data-region="山梨県" data-rating="4.4">
                    <div class="article-image">🍜
                        <div class="article-rating">⭐ 4.4</div>
                        <div class="article-stats">👁️ 1,492 💬 12</div>
                    </div>
                    <div class="article-content">
                        <div class="article-meta">
                            <span class="article-category">機能性成分</span>
                            <span>2025-01-08</span>
                        </div>
                        <h3 class="article-title">ほうとうの食物繊維と血糖値上昇抑制効果の臨床評価</h3>
                        <p class="article-description">山梨県のほうとうに含まれる水溶性・不溶性食物繊維の血糖値および血中脂質への影響を健常成人で評価しました。</p>
                        <div class="article-research">
                            <div class="research-title">🔬 主要な科学的知見</div>
                            <p>ほうとう摂取後の血糖値上昇が白米と比較して32%抑制され、食後血糖スパイクの改善効果を確認。</p>
                            <div class="research-citation">出典: 鈴木三郎 et al. (2025). 日本栄養・食糧学会誌, 78(1), 67-78.</div>
                        </div>
                        <div class="article-footer">
                            <div class="article-actions">
                                <button class="action-btn" onclick="toggleFavorite(this)">❤️ お気に入り</button>
                                <button class="action-btn" onclick="shareArticle(this)">📤 シェア</button>
                            </div>
                            <div class="comments-count">💬 12件のコメント</div>
                        </div>
                    </div>
                </div>

                <div class="article-card" data-category="地域比較" data-region="京都府" data-rating="4.7">
                    <div class="article-image">🥄
                        <div class="article-rating">⭐ 4.7</div>
                        <div class="article-stats">👁️ 1,346 💬 21</div>
                    </div>
                    <div class="article-content">
                        <div class="article-meta">
                            <span class="article-category">地域比較</span>
                            <span>2025-01-05</span>
                        </div>
                        <h3 class="article-title">茶碗蒸しの地域別レシピと栄養価の比較研究<span class="research-badge">査読済</span></h3>
                        <p class="article-description">全国7地域の茶碗蒸しレシピを比較し、具材の違いが栄養成分や機能性に与える影響を詳細に分析しました。</p>
                        <div class="article-research">
                            <div class="research-title">🔬 主要な科学的知見</div>
                            <p>京都式茶碗蒸しの銀杏添加により、ビタミンE含量が50%増加し、認知機能改善に寄与する可能性を示唆。</p>
                            <div class="research-citation">出典: 高橋美香 et al. (2025). 地域栄養学研究, 15(2), 134-147.</div>
                        </div>
                        <div class="article-footer">
                            <div class="article-actions">
                                <button class="action-btn" onclick="toggleFavorite(this)">❤️ お気に入り</button>
                                <button class="action-btn" onclick="shareArticle(this)">📤 シェア</button>
                            </div>
                            <div class="comments-count">💬 21件のコメント</div>
                        </div>
                    </div>
                </div>

                <div class="article-card" data-category="発酵食品" data-region="広島県" data-rating="4.3">
                    <div class="article-image">🥞
                        <div class="article-rating">⭐ 4.3</div>
                        <div class="article-stats">👁️ 1,156 💬 9</div>
                    </div>
                    <div class="article-content">
                        <div class="article-meta">
                            <span class="article-category">発酵食品</span>
                            <span>2025-01-03</span>
                        </div>
                        <h3 class="article-title">広島風お好み焼きの乳酸発酵と消化性の向上効果</h3>
                        <p class="article-description">お好み焼きの生地発酵過程で生成される乳酸菌が、小麦粉タンパク質の消化性と栄養価に与える影響を調査しました。</p>
                        <div class="article-research">
                            <div class="research-title">🔬 主要な科学的知見</div>
                            <p>24時間発酵により、タンパク質の in vitro 消化率が17%向上し、必須アミノ酸スコアも改善。</p>
                            <div class="research-citation">出典: 中村健一 et al. (2025). 発酵と食品, 42(3), 78-89.</div>
                        </div>
                        <div class="article-footer">
                            <div class="article-actions">
                                <button class="action-btn" onclick="toggleFavorite(this)">❤️ お気に入り</button>
                                <button class="action-btn" onclick="shareArticle(this)">📤 シェア</button>
                            </div>
                            <div class="comments-count">💬 9件のコメント</div>
                        </div>
                    </div>
                </div>
            </div>
        </section>
    </main>

    <footer style="background: rgba(0, 0, 0, 0.8); color: white; text-align: center; padding: 2rem 0; margin-top: 3rem;">
        <div class="container">
            <p>&copy; 2025 郷土料理科学研究所 - 科学的根拠に基づく食文化研究プラットフォーム</p>
            <p>🧪 論文・統計データ・コメント機能で科学的知見を共有</p>
        </div>
    </footer>

    <!-- 記事詳細モーダル -->
    <div id="articleModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <span class="close">&times;</span>
                <div id="modalTitle"></div>
            </div>
            <div class="modal-body">
                <div id="modalContent"></div>
                <div class="comments-section">
                    <h3>💬 研究コメント・ディスカッション</h3>
                    <div class="comment-form">
                        <h4>コメントを投稿</h4>
                        <input type="text" placeholder="お名前 (研究者名・所属)" style="width: 100%; padding: 8px; margin-bottom: 0.5rem; border: 1px solid #ddd; border-radius: 4px;">
                        <textarea class="comment-input" placeholder="研究に対するコメント、質問、追加情報などをお書きください..."></textarea>
                        <button class="btn btn-primary" onclick="addComment()">💬 コメント投稿</button>
                    </div>
                    <div class="comments-list" id="commentsList">
                        <div class="comment">
                            <div class="comment-header">
                                <div class="comment-author">田中研究員 (東京大学)</div>
                                <div class="comment-date">2時間前</div>
                            </div>
                            <div class="comment-text">発酵過程でのビタミンB12の増加について、追加の検証実験データはありますか？非常に興味深い研究で、我々の関連研究でも似たような傾向を確認しています。</div>
                        </div>
                        <div class="comment">
                            <div class="comment-header">
                                <div class="comment-author">佐藤栄養士 (管理栄養士)</div>
                                <div class="comment-date">5時間前</div>
                            </div>
                            <div class="comment-text">臨床現場での応用可能性が高い研究ですね。患者さんの栄養指導に活用させていただきたいと思います。レシピの標準化についてもご検討いただけると幸いです。</div>
                        </div>
                        <div class="comment">
                            <div class="comment-header">
                                <div class="comment-author">山田教授 (京都大学 食品科学科)</div>
                                <div class="comment-date">1日前</div>
                            </div>
                            <div class="comment-text">メタボローム解析の結果も合わせて公開していただけると、より包括的な理解が深まります。査読過程でのコメントも参考になりました。</div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // グローバル変数
        let articlesData = [];
        let analytics = {
            totalUsers: 8234,
            dailyUsers: 342,
            avgTime: '5:42',
            bounceRate: '23%',
            heroViews: 24891,
            heroPapers: 127,
            heroComments: 1847
        };

        // 初期化
        document.addEventListener('DOMContentLoaded', function() {
            initializeAnalytics();
            setupEventListeners();
            simulateRealTimeUpdates();
        });

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

        // 統計情報の初期化
        function initializeAnalytics() {
            document.getElementById('totalUsers').textContent = analytics.totalUsers.toLocaleString();
            document.getElementById('dailyUsers').textContent = analytics.dailyUsers.toLocaleString();
            document.getElementById('avgTime').textContent = analytics.avgTime;
            document.getElementById('bounceRate').textContent = analytics.bounceRate;
            document.getElementById('heroViews').textContent = analytics.heroViews.toLocaleString();
            document.getElementById('heroPapers').textContent = analytics.heroPapers.toLocaleString();
            document.getElementById('heroComments').textContent = analytics.heroComments.toLocaleString();
        }

        // イベントリスナーの設定
        function setupEventListeners() {
            // 記事投稿フォーム
            document.getElementById('articleForm').addEventListener('submit', function(e) {
                e.preventDefault();
                handleArticleSubmission();
            });

            // 検索機能
            document.getElementById('searchInput').addEventListener('input', function() {
                filterArticles();
            });

            // フィルターボタン
            document.querySelectorAll('.filter-btn').forEach(btn => {
                btn.addEventListener('click', function() {
                    toggleFilter(this);
                    filterArticles();
                });
            });

            // 記事カードクリック
            document.querySelectorAll('.article-card').forEach(card => {
                card.addEventListener('click', function() {
                    showArticleModal(this);
                });
            });

            // モーダル閉じる
            document.querySelector('.close').addEventListener('click', closeModal);
            window.addEventListener('click', function(event) {
                const modal = document.getElementById('articleModal');
                if (event.target === modal) {
                    closeModal();
                }
            });
        }

        // 記事投稿処理
        function handleArticleSubmission() {
            const formData = new FormData(document.getElementById('articleForm'));
            const articleData = {
                title: formData.get('title'),
                category: formData.get('category'),
                region: formData.get('region'),
                emoji: formData.get('emoji'),
                description: formData.get('description'),
                methodology: formData.get('methodology'),
                findings: formData.get('findings'),
                nutrition: formData.get('nutrition'),
                citations: formData.get('citations'),
                views: 0,
                comments: 0,
                rating: 4.0 + Math.random() * 0.8,
                dateCreated: new Date().toLocaleDateString('ja-JP')
            };

            addNewArticleCard(articleData);
            
            // 統計更新
            analytics.heroPapers++;
            document.getElementById('heroPapers').textContent = analytics.heroPapers;
            
            alert('📝 研究記事が正常に投稿されました！');
            clearForm();
        }

        // 新しい記事カードを追加
        function addNewArticleCard(data) {
            const articlesGrid = document.getElementById('articlesGrid');
            const newCard = document.createElement('div');
            newCard.className = 'article-card';
            newCard.setAttribute('data-category', data.category);
            newCard.setAttribute('data-region', data.region);
            newCard.setAttribute('data-rating', data.rating.toFixed(1));
            
            newCard.innerHTML = `
                <div class="article-image">${data.emoji}
                    <div class="article-rating">⭐ ${data.rating.toFixed(1)}</div>
                    <div class="article-stats">👁️ ${data.views} 💬 ${data.comments}</div>
                </div>
                <div class="article-content">
                    <div class="article-meta">
                        <span class="article-category">${data.category}</span>
                        <span>${data.dateCreated}</span>
                    </div>
                    <h3 class="article-title">${data.title}<span class="research-badge">新着</span></h3>
                    <p class="article-description">${data.description}</p>
                    <div class="article-research">
                        <div class="research-title">🔬 主要な科学的知見</div>
                        <p>${data.findings}</p>
                        <div class="research-citation">出典: ${data.citations}</div>
                    </div>
                    <div class="article-footer">
                        <div class="article-actions">
                            <button class="action-btn" onclick="toggleFavorite(this)">❤️ お気に入り</button>
                            <button class="action-btn" onclick="shareArticle(this)">📤 シェア</button>
                        </div>
                        <div class="comments-count">💬 ${data.comments}件のコメント</div>
                    </div>
                </div>
            `;
            
            articlesGrid.insertBefore(newCard, articlesGrid.firstChild);
            
            // クリックイベントを追加
            newCard.addEventListener('click', function() {
                showArticleModal(this);
            });
        }

        // フォームクリア
        function clearForm() {
            document.getElementById('articleForm').reset();
        }

        // フィルター切り替え
        function toggleFilter(button) {
            const filterType = button.getAttribute('data-filter') || button.getAttribute('data-region') || button.getAttribute('data-rating');
            const isActive = button.classList.contains('active');
            
            // 同じグループの他のボタンを非アクティブにする（単一選択の場合）
            const parentSection = button.closest('.filter-section');
            if (parentSection) {
                parentSection.querySelectorAll('.filter-btn').forEach(btn => {
                    if (btn !== button) btn.classList.remove('active');
                });
            }
            
            button.classList.toggle('active', !isActive);
        }

        // 記事フィルタリング
        function filterArticles() {
            const searchTerm = document.getElementById('searchInput').value.toLowerCase();
            const activeFilters = {
                category: getActiveFilter('data-filter'),
                region: getActiveFilter('data-region'),
                rating: getActiveFilter('data-rating')
            };
            
            const articleCards = document.querySelectorAll('.article-card');
            
            articleCards.forEach(card => {
                const matchesSearch = searchTerm === '' || 
                    card.textContent.toLowerCase().includes(searchTerm);
                
                const matchesCategory = activeFilters.category === 'all' || 
                    card.getAttribute('data-category') === activeFilters.category;
                
                const matchesRegion = activeFilters.region === 'all' || 
                    card.getAttribute('data-region') === activeFilters.region;
                
                const matchesRating = activeFilters.rating === 'all' || 
                    checkRatingFilter(card, activeFilters.rating);
                
                if (matchesSearch && matchesCategory && matchesRegion && matchesRating) {
                    card.style.display = 'block';
                    card.style.animation = 'fadeInUp 0.5s ease';
                } else {
                    card.style.display = 'none';
                }
            });
        }

        // アクティブフィルターを取得
        function getActiveFilter(dataAttribute) {
            const activeBtn = document.querySelector(`.filter-btn.active[${dataAttribute}]`);
            return activeBtn ? activeBtn.getAttribute(dataAttribute) : 'all';
        }

        // 評価フィルターチェック
        function checkRatingFilter(card, ratingFilter) {
            const rating = parseFloat(card.getAttribute('data-rating'));
            switch (ratingFilter) {
                case 'high': return rating >= 4.0;
                case 'popular': return parseInt(card.querySelector('.article-stats').textContent.match(/\d+/)[0]) > 2000;
                case 'recent': return true; // 簡略化: すべて最近として扱う
                default: return true;
            }
        }

        // 記事詳細モーダル表示
        function showArticleModal(card) {
            const modal = document.getElementById('articleModal');
            const title = card.querySelector('.article-title').textContent;
            const content = card.querySelector('.article-content').innerHTML;
            
            document.getElementById('modalTitle').innerHTML = `<h2>${title}</h2>`;
            document.getElementById('modalContent').innerHTML = content;
            
            modal.style.display = 'block';
            document.body.style.overflow = 'hidden';
            
            // 閲覧数を増加
            updateViewCount(card);
        }

        // モーダル閉じる
        function closeModal() {
            const modal = document.getElementById('articleModal');
            modal.style.display = 'none';
            document.body.style.overflow = 'auto';
        }

        // 閲覧数更新
        function updateViewCount(card) {
            const statsElement = card.querySelector('.article-stats');
            const currentViews = parseInt(statsElement.textContent.match(/👁️ (\d+)/)[1]);
            const newViews = currentViews + 1;
            statsElement.textContent = statsElement.textContent.replace(/👁️ \d+/, `👁️ ${newViews}`);
            
            // 全体統計も更新
            analytics.heroViews++;
            document.getElementById('heroViews').textContent = analytics.heroViews.toLocaleString();
        }

        // お気に入り切り替え
        function toggleFavorite(button) {
            const isFavorited = button.classList.contains('favorited');
            if (isFavorited) {
                button.innerHTML = '❤️ お気に入り';
                button.classList.remove('favorited');
            } else {
                button.innerHTML = '💖 お気に入り済み';
                button.classList.add('favorited');
            }
        }

        // 記事シェア
        function shareArticle(button) {
            const articleCard = button.closest('.article-card');
            const title = articleCard.querySelector('.article-title').textContent;
            
            if (navigator.share) {
                navigator.share({
                    title: title,
                    text: '郷土料理科学研究所の研究記事をシェア',
                    url: window.location.href
                });
            } else {
                // フォールバック: クリップボードにコピー
                navigator.clipboard.writeText(`${title} - ${window.location.href}`);
                alert('📎 記事リンクをクリップボードにコピーしました！');
            }
        }

        // コメント追加
        function addComment() {
            const commentsList = document.getElementById('commentsList');
            const commentInput = document.querySelector('.comment-input');
            const nameInput = document.querySelector('input[placeholder*="お名前"]');
            
            if (commentInput.value.trim() && nameInput.value.trim()) {
                const newComment = document.createElement('div');
                newComment.className = 'comment';
                newComment.innerHTML = `
                    <div class="comment-header">
                        <div class="comment-author">${nameInput.value}</div>
                        <div class="comment-date">たった今</div>
                    </div>
                    <div class="comment-text">${commentInput.value}</div>
                `;
                
                commentsList.insertBefore(newComment, commentsList.firstChild);
                
                // フォームクリア
                commentInput.value = '';
                nameInput.value = '';
                
                // コメント数更新
                analytics.heroComments++;
                document.getElementById('heroComments').textContent = analytics.heroComments.toLocaleString();
                
                alert('💬 コメントが投稿されました！');
            } else {
                alert('お名前とコメント内容を入力してください。');
            }
        }

        // 記事編集
        function editArticle(articleId) {
            alert('📝 編集機能：選択された記事の編集画面に移動します');
        }

        // 記事削除
        function deleteArticle(articleId) {
            if (confirm('🗑️ この記事を削除してもよろしいですか？')) {
                alert('記事が削除されました');
            }
        }

        // リアルタイム統計更新シミュレーション
        function simulateRealTimeUpdates() {
            setInterval(() => {
                // 統計をランダムに更新
                analytics.dailyUsers += Math.floor(Math.random() * 5);
                analytics.heroViews += Math.floor(Math.random() * 10);
                
                document.getElementById('dailyUsers').textContent = analytics.dailyUsers.toLocaleString();
                document.getElementById('heroViews').textContent = analytics.heroViews.toLocaleString();
            }, 30000); // 30秒ごと
        }

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

        // ヘッダーのスクロール効果
        window.addEventListener('scroll', function() {
            const header = document.querySelector('header');
            if (window.scrollY > 100) {
                header.style.background = 'rgba(255, 255, 255, 0.98)';
                header.style.boxShadow = '0 2px 30px rgba(0, 0, 0, 0.15)';
            } else {
                header.style.background = 'rgba(255, 255, 255, 0.95)';
                header.style.boxShadow = '0 2px 20px rgba(0, 0, 0, 0.1)';
            }
        });
    </script>
</body>
</html>
