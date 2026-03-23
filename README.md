<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{{ user.name }} - 个人主页</title>
    <!-- 引入谷歌字体 -->
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+SC:wght@300;400;700&display=swap" rel="stylesheet">
    <!-- 引入图标库 -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    
    <style>
        :root {
            --primary-color: #6a11cb;
            --secondary-color: #2575fc;
            --text-color: #333;
            --bg-color: #f4f7f6;
            --card-bg: rgba(255, 255, 255, 0.95);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Noto Sans SC', sans-serif;
            background: linear-gradient(135deg, var(--primary-color) 0%, var(--secondary-color) 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            color: var(--text-color);
            padding: 20px;
        }

        .container {
            background: var(--card-bg);
            width: 100%;
            max-width: 900px;
            border-radius: 20px;
            box-shadow: 0 20px 50px rgba(0,0,0,0.2);
            overflow: hidden;
            display: flex;
            flex-direction: column;
            animation: fadeIn 1s ease-out;
        }

        @media (min-width: 768px) {
            .container {
                flex-direction: row;
            }
        }

        /* 左侧个人信息区 */
        .profile-section {
            background: linear-gradient(135deg, #ffffff 0%, #f0f0f0 100%);
            padding: 40px;
            text-align: center;
            flex: 1;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            border-right: 1px solid #eee;
        }

        .avatar {
            width: 150px;
            height: 150px;
            border-radius: 50%;
            object-fit: cover;
            border: 5px solid white;
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
            margin-bottom: 20px;
            background-color: #ddd; /* 占位色 */
        }

        .name {
            font-size: 2rem;
            font-weight: 700;
            margin-bottom: 10px;
            color: var(--primary-color);
        }

        .school {
            font-size: 1.1rem;
            color: #666;
            margin-bottom: 5px;
        }

        .major {
            font-size: 0.95rem;
            color: #888;
            margin-bottom: 20px;
        }

        .tags {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 10px;
        }

        .tag {
            background: #eef2ff;
            color: var(--primary-color);
            padding: 5px 15px;
            border-radius: 20px;
            font-size: 0.85rem;
            font-weight: 600;
        }

        /* 右侧详细内容区 */
        .details-section {
            padding: 40px;
            flex: 1.5;
        }

        .section-title {
            font-size: 1.5rem;
            margin-bottom: 20px;
            position: relative;
            display: inline-block;
            color: #333;
        }

        .section-title::after {
            content: '';
            position: absolute;
            left: 0;
            bottom: -5px;
            width: 40px;
            height: 3px;
            background: var(--secondary-color);
            border-radius: 2px;
        }

        .info-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }

        .info-card {
            background: #fff;
            padding: 20px;
            border-radius: 12px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.05);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        .info-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(0,0,0,0.1);
        }

        .info-card h3 {
            font-size: 1.1rem;
            margin-bottom: 15px;
            color: var(--secondary-color);
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .skill-list, .hobby-list {
            list-style: none;
        }

        .skill-list li, .hobby-list li {
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 10px;
            color: #555;
        }

        .skill-list li i, .hobby-list li i {
            color: var(--primary-color);
            width: 20px;
            text-align: center;
        }

        .contact-btn {
            display: inline-block;
            margin-top: 20px;
            padding: 12px 30px;
            background: linear-gradient(90deg, var(--primary-color), var(--secondary-color));
            color: white;
            text-decoration: none;
            border-radius: 30px;
            font-weight: bold;
            transition: opacity 0.3s;
            box-shadow: 0 5px 15px rgba(37, 117, 252, 0.4);
        }

        .contact-btn:hover {
            opacity: 0.9;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* 移动端适配调整 */
        @media (max-width: 768px) {
            .profile-section {
                border-right: none;
                border-bottom: 1px solid #eee;
            }
        }
    </style>
</head>
<body>

    <div class="container">
        <!-- 左侧：头像与基本信息 -->
        <div class="profile-section">
            <!-- 请替换下面的 src 为你的真实照片链接，或者本地路径如 'static/me.jpg' -->
            <img C:\Users\35379\Desktop\作业\Python课\头像.jpg="https://ui-avatars.com/api/?name={{ user.name }}&background=6a11cb&color=fff&size=256" alt="Avatar" class="avatar">
            
            <h1 class="name">{{ user.name }}</h1>
            <p class="school"><i class="fas fa-university"></i> {{ user.university }}</p>
            <p class="major">{{ user.major }}</p>
            
            <div class="tags">
                {% for trait in user.traits %}
                <span class="tag">#{{ trait }}</span>
                {% endfor %}
            </div>
        </div>

        <!-- 右侧：技能与爱好 -->
        <div class="details-section">
            <div class="info-grid">
                <!-- 技能卡片 -->
                <div class="info-card">
                    <h3><i class="fas fa-laptop-code"></i> 技能 Skills</h3>
                    <ul class="skill-list">
                        {% for skill in user.skills %}
                        <li><i class="fas fa-check-circle"></i> {{ skill }}</li>
                        {% endfor %}
                    </ul>
                </div>

                <!-- 爱好卡片 -->
                <div class="info-card">
                    <h3><i class="fas fa-heart"></i> 爱好 Hobbies</h3>
                    <ul class="hobby-list">
                        {% for hobby in user.hobbies %}
                        <li><i class="fas fa-star"></i> {{ hobby }}</li>
                        {% endfor %}
                    </ul>
                </div>
            </div>

            <div style="margin-top: 30px;">
                <p style="line-height: 1.6; color: #555;">
                    你好！我是一名来自华东政法大学的金融专业学生。我性格幽默随和，热爱探索新事物。
                    目前正在努力学习各种技能，从编程到运动，希望能结识更多有趣的朋友！
                </p>
                <a href="mailto:your-email@example.com" class="contact-btn">联系我</a>
            </div>
        </div>
    </div>

</body>
</html>
