index.html
 <!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>郷土料理科学研究所 - コメント機能付き完全版</title>
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
        
        /* 成功メッセージ */
        .success-message {
            background: #4CAF50;
            color: white;
            padding: 1rem;
            border-radius: 8px;
            margin: 1rem 0;
            text-align: center;
            display: none;
            animation: slideDown 0.5s ease;
        }
        
        @keyframes slideDown {
            from { opacity: 0; transform: translateY(-20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        /* 保存状態インジケーター */
        .save-indicator {
            position: fixed;
            top: 100px;
            right: 20px;
            background: #4CAF50;
            color: white;
            padding: 10px 15px;
            border-radius: 25px;
            font-size: 0.9rem;
            display: none;
            z-index: 1001;
            animation: fadeInRight 0.5s ease;
        }
        
        @keyframes fadeInRight {
            from { opacity: 0; transform: translateX(50px); }
            to { opacity: 1; transform: translateX(0); }
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
        
        .nutrition-section {
            background: #f0f9ff;
            padding: 1rem;
            border-radius: 10px;
            border-left: 4px solid #10b981;
            margin: 1rem 0;
        }
        
        .nutrition-title {
            font-weight: bold;
            font-size: 0.9rem;
            color: #047857;
            margin-bottom: 0.5rem;
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
            color: #667eea;
            font-size: 0.9rem;
            font-weight: bold;
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
            position: relative;
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
        
        .comment-input-group {
            margin-bottom: 1rem;
        }
        
        .comment-input-group input,
        .comment-input-group textarea {
            width: 100%;
            padding: 12px;
            border: 2px solid #e2e8f0;
            border-radius: 8px;
            margin-bottom: 0.5rem;
        }
        
        .comment-input-group textarea {
            min-height: 100px;
            resize: vertical;
        }
        
        .comment-input-group input:focus,
        .comment-input-group textarea:focus {
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
            
            .modal-content {
                width: 95%;
                margin: 5% auto;
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
        
        .auto-save-badge {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
            padding: 3px 8px;
            border-radius: 12px;
            font-size: 0.7rem;
            font-weight: bold;
            margin-left: 0.5rem;
        }
        
        .comment-badge {
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

    <!-- 自動保存インジケーター -->
    <div class="save-indicator" id="saveIndicator">
        ✅ 記事が自動保存されました
    </div>

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
                    <span class="hero-stat-label">投稿論文数</span>
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
                <button class="admin-tab" onclick="switchTab('backup')">💾 バックアップ</button>
            </div>

            <!-- 記事投稿タブ -->
            <div id="create-tab" class="tab-content active">
                <h3>✏️ 新しい研究記事を投稿 <span class="auto-save-badge">自動保存</span><span class="comment-badge">コメント機能</span></h3>
                
                <div class="success-message" id="successMessage">
                    🎉 記事が正常に投稿・保存されました！
                </div>
                
                <form id="articleForm">
                    <div class="form-group">
                        <label for="title">記事タイトル *</label>
                        <input type="text" id="title" name="title" placeholder="例：味噌の発酵過程における機能性成分の変化" required>
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
                        <label for="description">研究概要 *</label>
                        <textarea id="description" name="description" placeholder="この研究の目的、方法、主要な発見について簡潔に説明してください..." required></textarea>
                    </div>
                    
                    <div class="form-group">
                        <label for="findings">主要な発見 *</label>
                        <textarea id="findings" name="findings" placeholder="研究で得られた主要な結果、科学的知見について説明してください..." required></textarea>
                    </div>
                    
                    <div class="form-group">
                        <label for="nutrition">栄養・成分データ</label>
                        <textarea id="nutrition" name="nutrition" placeholder="例：タンパク質: 18.5g/100g, ビタミンB1: 0.8mg/100g, 食物繊維: 3.2g/100g"></textarea>
                    </div>
                    
                    <button type="submit" class="btn btn-primary">📝 研究記事を投稿・自動保存</button>
                    <button type="button" class="btn btn-secondary" onclick="clearForm()">🗑️ クリア</button>
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
                        <div>保存済み記事数</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-number" id="totalCommentsCount">0</div>
                        <div>総コメント数</div>
                    </div>
                </div>
                <p style="text-align: center; color: #666; margin-top: 2rem;">
                    📝 記事投稿・コメント投稿で統計データが自動更新されます
                </p>
            </div>

            <!-- 管理タブ -->
            <div id="manage-tab" class="tab-content">
                <h3>📝 記事管理 <span class="auto-save-badge">自動保存中</span></h3>
                <div id="articleList">
                    <p style="text-align: center; color: #666; margin: 2rem 0;" id="noArticlesMessage">
                        まだ記事が投稿されていません。<br>
                        「✏️ 記事投稿」タブから最初の記事を投稿してみましょう！
                    </p>
                </div>
            </div>

            <!-- バックアップタブ -->
            <div id="backup-tab" class="tab-content">
                <h3>💾 データバックアップ・復元</h3>
                
                <div style="background: #f8f9ff; padding: 1.5rem; border-radius: 15px; margin: 1rem 0; border-left: 4px solid #667eea;">
                    <h4>📊 現在保存されているデータ</h4>
                    <p>投稿された記事データとコメントは自動的にブラウザに保存されています。</p>
                    <div style="background: #fff; padding: 1rem; border-radius: 8px; margin-top: 1rem; border: 1px solid #e2e8f0; font-family: monospace; font-size: 0.9rem; max-height: 200px; overflow-y: auto;" id="backupData">
                        記事データがここに表示されます...
                    </div>
                    <button class="btn btn-primary" onclick="exportData()">📥 データをダウンロード</button>
                    <button class="btn btn-secondary" onclick="clearAllData()">🗑️ 全データクリア</button>
                </div>
            </div>
        </section>

        <!-- 検索セクション -->
        <section id="search" class="search-section">
            <div class="search-header">
                <h2>🔍 研究検索</h2>
                <p>投稿された論文・記事から検索</p>
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
                <p class="section-subtitle">科学的根拠に基づく郷土料理研究 - コメント機能付き</p>
            </div>
            
            <div class="articles-grid" id="articlesGrid">
                <!-- 記事が投稿されると自動的にここに表示されます -->
            </div>
        </section>
    </main>

    <footer style="background: rgba(0, 0, 0, 0.8); color: white; text-align: center; padding: 2rem 0; margin-top: 3rem;">
        <div class="container">
            <p>&copy; 2025 郷土料理科学研究所 - コメント機能付き研究プラットフォーム</p>
            <p>🧪 記事・コメントは自動的に保存され、読者と研究者が交流できます</p>
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
                        <div class="comment-input-group">
                            <input type="text" id="commentAuthor" placeholder="お名前 (研究者名・所属など)" required>
                            <textarea id="commentText" placeholder="研究に対するコメント、質問、追加情報などをお書きください..." required></textarea>
                            <button class="btn btn-primary" onclick="addComment()">💬 コメント投稿</button>
                        </div>
                    </div>
                    <div class="comments-list" id="commentsList">
                        <!-- コメントがここに動的に追加されます -->
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // 記事データを保存するためのオブジェクト
        const articleStorage = {
            save: function(articles) {
                try {
                    const data = JSON.stringify(articles);
                    localStorage.setItem('research_articles', data);
                    localStorage.setItem('last_save_time', new Date().toISOString());
                    this.showSaveIndicator();
                    return true;
                } catch (error) {
                    console.error('保存エラー:', error);
                    return false;
                }
            },
            
            load: function() {
                try {
                    const data = localStorage.getItem('research_articles');
                    return data ? JSON.parse(data) : [];
                } catch (error) {
                    console.error('読み込みエラー:', error);
                    return [];
                }
            },
            
            showSaveIndicator: function() {
                const indicator = document.getElementById('saveIndicator');
                indicator.style.display = 'block';
                setTimeout(() => {
                    indicator.style.display = 'none';
                }, 3000);
            }
        };

        // グローバル変数
        let articles = [];
        let currentArticleIndex = -1;

        // 初期化
        document.addEventListener('DOMContentLoaded', function() {
            loadSavedArticles();
            updateStatistics();
            setupEventListeners();
            updateBackupDisplay();
        });

        // 保存された記事を読み込み
        function loadSavedArticles() {
            articles = articleStorage.load();
            displayArticles();
            updateStatistics();
        }

        // 記事を表示
        function displayArticles() {
            const articlesGrid = document.getElementById('articlesGrid');
            
            if (articles.length === 0) {
                articlesGrid.innerHTML = `
                    <div style="text-align: center; color: #666; padding: 3rem; grid-column: 1/-1;">
                        <h3>📝 最初の記事を投稿してみましょう！</h3>
                        <p>管理画面の「✏️ 記事投稿」から研究記事を追加できます</p>
                        <button class="btn btn-primary" onclick="toggleAdminPanel()" style="margin-top: 1rem;">
                            📊 管理画面を開く
                        </button>
                    </div>
                `;
                return;
            }
            
            articlesGrid.innerHTML = '';
            
            articles.forEach((article, index) => {
                const articleCard = createArticleCard(article, index);
                articlesGrid.appendChild(articleCard);
            });
        }

        // 記事カードを作成
        function createArticleCard(article, index) {
            const card = document.createElement('div');
            card.className = 'article-card';
            card.setAttribute('data-region', article.region);
            
            const commentsCount = article.comments ? article.comments.length : 0;
            
            card.innerHTML = `
                <div class="article-image">${article.emoji || '📄'}
                    <div class="article-rating">⭐ ${article.rating || 5.0}</div>
                    <div class="article-stats">👁️ ${article.views || 1} 💬 ${commentsCount}</div>
                </div>
                <div class="article-content">
                    <div class="article-meta">
                        <span class="article-category">研究記事</span>
                        <span>${article.dateCreated}</span>
                    </div>
                    <h3 class="article-title">${article.title}<span class="research-badge">コメント可</span></h3>
                    <p class="article-description">${article.description}</p>
                    <div class="article-research">
                        <div class="research-title">🔬 主要な科学的知見</div>
                        <p>${article.findings}</p>
                    </div>
                    ${article.nutrition ? `
                    <div class="nutrition-section">
                        <div class="nutrition-title">🧪 栄養・成分データ</div>
                        <p>${article.nutrition}</p>
                    </div>
                    ` : ''}
                    <div class="article-footer">
                        <div class="article-actions">
                            <button class="action-btn" onclick="editArticle(${index})">✏️ 編集</button>
                            <button class="action-btn" onclick="deleteArticle(${index})">🗑️ 削除</button>
                        </div>
                        <div class="comments-count" onclick="showArticleModal(${index})">💬 ${commentsCount}件のコメント</div>
                    </div>
                </div>
            `;
            
            // カード全体クリックでモーダル表示
            card.addEventListener('click', function(e) {
                // 編集・削除ボタンをクリックした場合はモーダルを開かない
                if (!e.target.classList.contains('action-btn')) {
                    showArticleModal(index);
                }
            });
            
            return card;
        }

        // 記事詳細モーダル表示
        function showArticleModal(index) {
            const article = articles[index];
            if (!article) return;
            
            currentArticleIndex = index;
            
            const modal = document.getElementById('articleModal');
            const modalTitle = document.getElementById('modalTitle');
            const modalContent = document.getElementById('modalContent');
            
            modalTitle.innerHTML = `<h2>${article.title}</h2>`;
            
            modalContent.innerHTML = `
                <div class="article-meta" style="margin-bottom: 1rem;">
                    <span class="article-category">研究記事</span>
                    <span>地域: ${article.region} | 投稿日: ${article.dateCreated}</span>
                </div>
                <div style="margin-bottom: 2rem;">
                    <h3>📋 研究概要</h3>
                    <p style="line-height: 1.6;">${article.description}</p>
                </div>
                <div style="margin-bottom: 2rem;">
                    <h3>🔬 主要な科学的知見</h3>
                    <p style="line-height: 1.6;">${article.findings}</p>
                </div>
                ${article.nutrition ? `
                <div style="margin-bottom: 2rem;">
                    <h3>🧪 栄養・成分データ</h3>
                    <p style="line-height: 1.6; background: #f0f9ff; padding: 1rem; border-radius: 8px;">${article.nutrition}</p>
                </div>
                ` : ''}
                <div style="background: #f8f9ff; padding: 1rem; border-radius: 8px; margin-bottom: 1rem;">
                    <h4>📊 記事統計</h4>
                    <p>閲覧数: ${article.views || 1} | コメント: ${article.comments ? article.comments.length : 0}件 | 評価: ⭐${article.rating || 5.0}</p>
                </div>
            `;
            
            // コメントを表示
            displayComments(article.comments || []);
            
            modal.style.display = 'block';
            document.body.style.overflow = 'hidden';
            
            // 閲覧数を増加
            updateViewCount(index);
        }

        // コメント表示
        function displayComments(comments) {
            const commentsList = document.getElementById('commentsList');
            
            if (comments.length === 0) {
                commentsList.innerHTML = `
                    <p style="text-align: center; color: #666; margin: 2rem 0;">
                        まだコメントがありません。最初のコメントを投稿してみましょう！
                    </p>
                `;
                return;
            }
            
            commentsList.innerHTML = comments.map(comment => `
                <div class="comment">
                    <div class="comment-header">
                        <div class="comment-author">${comment.author}</div>
                        <div class="comment-date">${comment.date}</div>
                    </div>
                    <div class="comment-text">${comment.text}</div>
                </div>
            `).join('');
        }

        // コメント追加
        function addComment() {
            const authorInput = document.getElementById('commentAuthor');
            const textInput = document.getElementById('commentText');
            
            const author = authorInput.value.trim();
            const text = textInput.value.trim();
            
            if (!author || !text) {
                alert('お名前とコメント内容を入力してください。');
                return;
            }
            
            if (currentArticleIndex === -1) return;
            
            const newComment = {
                id: Date.now(),
                author: author,
                text: text,
                date: new Date().toLocaleString('ja-JP'),
                timestamp: new Date().toISOString()
            };
            
            // 記事にコメントを追加
            if (!articles[currentArticleIndex].comments) {
                articles[currentArticleIndex].comments = [];
            }
            articles[currentArticleIndex].comments.push(newComment);
            
            // データを保存
            articleStorage.save(articles);
            
            // 表示を更新
            displayComments(articles[currentArticleIndex].comments);
            displayArticles();
            updateStatistics();
            
            // フォームをクリア
            authorInput.value = '';
            textInput.value = '';
            
            alert('💬 コメントが投稿されました！');
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
                id: Date.now(),
                title: formData.get('title'),
                region: formData.get('region'),
                emoji: formData.get('emoji'),
                description: formData.get('description'),
                findings: formData.get('findings'),
                nutrition: formData.get('nutrition'),
                views: 1,
                comments: [],
                rating: 5.0,
                dateCreated: new Date().toLocaleDateString('ja-JP'),
                timeCreated: new Date().toISOString()
            };
            
            if (articleData.title && articleData.description && articleData.findings) {
                // 記事を配列に追加
                articles.unshift(articleData);
                
                // 自動保存
                const saved = articleStorage.save(articles);
                
                if (saved) {
                    // 表示を更新
                    displayArticles();
                    updateStatistics();
                    updateArticleManagement();
                    
                    // 成功メッセージ表示
                    showSuccessMessage();
                    clearForm();
                } else {
                    alert('❌ 保存に失敗しました。もう一度お試しください。');
                }
            } else {
                alert('❗ タイトル、研究概要、主要な発見は必須項目です。');
            }
        }

        // 成功メッセージ表示
        function showSuccessMessage() {
            const message = document.getElementById('successMessage');
            message.style.display = 'block';
            setTimeout(() => {
                message.style.display = 'none';
            }, 5000);
        }

        // 統計更新
        function updateStatistics() {
            const totalComments = articles.reduce((sum, article) => sum + (article.comments ? article.comments.length : 0), 0);
            
            document.getElementById('heroPapers').textContent = articles.length;
            document.getElementById('totalArticles').textContent = articles.length;
            document.getElementById('heroComments').textContent = totalComments;
            document.getElementById('totalCommentsCount').textContent = totalComments;
            
            const totalViews = articles.reduce((sum, article) => sum + (article.views || 1), 0);
            document.getElementById('heroViews').textContent = totalViews;
        }

        // 閲覧数更新
        function updateViewCount(index) {
            if (articles[index]) {
                articles[index].views = (articles[index].views || 1) + 1;
                articleStorage.save(articles);
                updateStatistics();
            }
        }

        // 記事管理画面更新
        function updateArticleManagement() {
            const articleList = document.getElementById('articleList');
            const noArticlesMessage = document.getElementById('noArticlesMessage');
            
            if (articles.length === 0) {
                if (noArticlesMessage) {
                    noArticlesMessage.style.display = 'block';
                }
                return;
            }
            
            if (noArticlesMessage) {
                noArticlesMessage.style.display = 'none';
            }
            
            articleList.innerHTML = articles.map((article, index) => {
                const commentsCount = article.comments ? article.comments.length : 0;
                return `
                    <div class="article-item" style="border: 1px solid #e2e8f0; padding: 1rem; margin: 1rem 0; border-radius: 8px;">
                        <h4>${article.title} <span style="color: #667eea;">(閲覧数: ${article.views || 1}, コメント: ${commentsCount}件)</span></h4>
                        <p>地域: ${article.region} | 投稿日: ${article.dateCreated}</p>
                        <button class="btn btn-primary" onclick="editArticle(${index})">✏️ 編集</button>
                        <button class="btn btn-secondary" onclick="deleteArticle(${index})">🗑️ 削除</button>
                        <button class="btn btn-primary" onclick="showArticleModal(${index})" style="background: #10b981;">💬 コメント確認</button>
                    </div>
                `;
            }).join('');
        }

        // 記事編集
        function editArticle(index) {
            const article = articles[index];
            if (!article) return;
            
            // フォームに記事データを設定
            document.getElementById('title').value = article.title;
            document.getElementById('region').value = article.region;
            document.getElementById('emoji').value = article.emoji || '';
            document.getElementById('description').value = article.description;
            document.getElementById('findings').value = article.findings;
            document.getElementById('nutrition').value = article.nutrition || '';
            
            // 記事投稿タブに切り替え
            switchTab('create');
            toggleAdminPanel();
            
            // 元の記事を削除（編集のため）
            articles.splice(index, 1);
            articleStorage.save(articles);
            displayArticles();
            updateStatistics();
            updateArticleManagement();
            
            alert('📝 記事データをフォームに読み込みました。編集して再投稿してください。');
        }

        // 記事削除
        function deleteArticle(index) {
            const article = articles[index];
            if (!article) return;
            
            const commentsCount = article.comments ? article.comments.length : 0;
            const confirmMessage = commentsCount > 0 
                ? `🗑️ 「${article.title}」を削除してもよろしいですか？\n※ ${commentsCount}件のコメントも一緒に削除されます。`
                : `🗑️ 「${article.title}」を削除してもよろしいですか？`;
            
            if (confirm(confirmMessage)) {
                articles.splice(index, 1);
                articleStorage.save(articles);
                displayArticles();
                updateStatistics();
                updateArticleManagement();
                alert('✅ 記事が削除されました。');
            }
        }

        // データエクスポート
        function exportData() {
            const totalComments = articles.reduce((sum, article) => sum + (article.comments ? article.comments.length : 0), 0);
            
            const data = {
                articles: articles,
                exportDate: new Date().toISOString(),
                totalArticles: articles.length,
                totalComments: totalComments,
                version: '2.0'
            };
            
            const blob = new Blob([JSON.stringify(data, null, 2)], { type: 'application/json' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `research_articles_with_comments_${new Date().toISOString().split('T')[0]}.json`;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            URL.revokeObjectURL(url);
            
            alert('📥 記事データ（コメント含む）がダウンロードされました！');
        }

        // バックアップ表示更新
        function updateBackupDisplay() {
            const backupData = document.getElementById('backupData');
            if (articles.length > 0) {
                const summary = {
                    記事数: articles.length,
                    総コメント数: articles.reduce((sum, article) => sum + (article.comments ? article.comments.length : 0), 0),
                    最新記事: articles[0] ? articles[0].title : 'なし',
                    最終更新: new Date().toLocaleString('ja-JP')
                };
                backupData.textContent = JSON.stringify(summary, null, 2);
            } else {
                backupData.textContent = '保存された記事データはまだありません。';
            }
        }

        // 全データクリア
        function clearAllData() {
            if (confirm('⚠️ 全ての記事データとコメントを削除してもよろしいですか？この操作は取り消せません。')) {
                if (confirm('🚨 本当に削除しますか？バックアップは取得済みですか？')) {
                    localStorage.removeItem('research_articles');
                    localStorage.removeItem('last_save_time');
                    articles = [];
                    displayArticles();
                    updateStatistics();
                    updateArticleManagement();
                    updateBackupDisplay();
                    alert('✅ 全データが削除されました。');
                }
            }
        }

        // モーダル閉じる
        function closeModal() {
            const modal = document.getElementById('articleModal');
            modal.style.display = 'none';
            document.body.style.overflow = 'auto';
            currentArticleIndex = -1;
        }

        // フィルター切り替え
        function toggleFilter(button) {
            const parentSection = button.closest('.filter-buttons');
            if (parentSection) {
                parentSection.querySelectorAll('.filter-btn').forEach(btn => {
                    btn.classList.remove('active');
                });
            }
            button.classList.add('active');
        }

        // 記事フィルタリング
        function filterArticles() {
            const searchTerm = document.getElementById('searchInput').value.toLowerCase();
            const activeFilter = document.querySelector('.filter-btn.active').getAttribute('data-filter');
            
            const articleCards = document.querySelectorAll('.article-card');
            
            articleCards.forEach(card => {
                const matchesSearch = searchTerm === '' || 
                    card.textContent.toLowerCase().includes(searchTerm);
                
                const matchesRegion = activeFilter === 'all' || 
                    card.getAttribute('data-region') === activeFilter;
                
                if (matchesSearch && matchesRegion) {
                    card.style.display = 'block';
                } else {
                    card.style.display = 'none';
                }
            });
        }

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
            
            // タブが選択された場合の処理
            if (tabName === 'manage') {
                updateArticleManagement();
            } else if (tabName === 'backup') {
                updateBackupDisplay();
            }
        }

        // フォームクリア
        function clearForm() {
            document.getElementById('articleForm').reset();
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

        // 初期表示で記事管理リストを更新
        setTimeout(() => {
            updateArticleManagement();
            updateBackupDisplay();
        }, 1000);
    </script>
</body>
</html>
