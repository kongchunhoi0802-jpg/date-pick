# date-pick
<!DOCTYPE html>
<html lang="zh-HK">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>💕 今日去邊度約會？</title>
    <style>
        :root {
            --bg: #fff5f5;
            --card-bg: #ffffff;
            --primary: #e8536c;
            --primary-light: #ffe0e5;
            --primary-dark: #c0394b;
            --accent: #f9a66c;
            --accent-light: #fff3e6;
            --green: #4caf84;
            --green-light: #e8f5e9;
            --yellow: #f0b94d;
            --yellow-light: #fff9ee;
            --orange: #f08060;
            --orange-light: #fff1ed;
            --text: #3d2c2c;
            --text-light: #7a6a6a;
            --text-muted: #b0a0a0;
            --border: #f0e0e0;
            --shadow-sm: 0 1px 3px rgba(0, 0, 0, 0.04), 0 1px 2px rgba(0, 0, 0, 0.03);
            --shadow: 0 4px 16px rgba(0, 0, 0, 0.06), 0 2px 6px rgba(0, 0, 0, 0.04);
            --shadow-lg: 0 12px 40px rgba(0, 0, 0, 0.1), 0 4px 12px rgba(0, 0, 0, 0.06);
            --shadow-xl: 0 20px 60px rgba(0, 0, 0, 0.15), 0 8px 20px rgba(0, 0, 0, 0.08);
            --radius-sm: 10px;
            --radius: 16px;
            --radius-lg: 22px;
            --radius-xl: 28px;
            --transition: 0.25s cubic-bezier(0.4, 0, 0.2, 1);
            --font: 'Segoe UI', 'PingFang HK', 'Microsoft JhengHei', 'Noto Sans HK', system-ui, -apple-system, sans-serif;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        html {
            scroll-behavior: smooth;
        }

        body {
            font-family: var(--font);
            background: var(--bg);
            color: var(--text);
            min-height: 100vh;
            line-height: 1.6;
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
            background-image:
                radial-gradient(ellipse at 20% 10%, rgba(232, 83, 108, 0.04) 0%, transparent 60%),
                radial-gradient(ellipse at 80% 90%, rgba(249, 166, 108, 0.05) 0%, transparent 60%),
                radial-gradient(ellipse at 50% 50%, rgba(255, 200, 180, 0.03) 0%, transparent 70%);
        }

        /* ===== Header ===== */
        .header {
            background: var(--card-bg);
            border-bottom: 1px solid var(--border);
            padding: 16px 24px;
            position: sticky;
            top: 0;
            z-index: 100;
            box-shadow: var(--shadow-sm);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            background: rgba(255, 255, 255, 0.92);
        }
        .header-inner {
            max-width: 1100px;
            margin: 0 auto;
            display: flex;
            align-items: center;
            justify-content: space-between;
            flex-wrap: wrap;
            gap: 10px;
        }
        .logo {
            display: flex;
            align-items: center;
            gap: 10px;
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--primary);
            letter-spacing: -0.3px;
            user-select: none;
        }
        .logo .heart {
            display: inline-block;
            animation: heartbeat 1.2s ease-in-out infinite;
            font-size: 1.6rem;
        }
        @keyframes heartbeat {
            0%,
            100% {
                transform: scale(1);
            }
            15% {
                transform: scale(1.25);
            }
            30% {
                transform: scale(1);
            }
            45% {
                transform: scale(1.2);
            }
            60% {
                transform: scale(1);
            }
        }
        .header-actions {
            display: flex;
            gap: 8px;
            flex-wrap: wrap;
        }
        .btn {
            display: inline-flex;
            align-items: center;
            gap: 6px;
            padding: 9px 16px;
            border-radius: 50px;
            font-size: 0.9rem;
            font-weight: 600;
            cursor: pointer;
            border: none;
            font-family: var(--font);
            transition: var(--transition);
            white-space: nowrap;
            letter-spacing: 0.2px;
            user-select: none;
            -webkit-tap-highlight-color: transparent;
            position: relative;
            overflow: hidden;
        }
        .btn:active {
            transform: scale(0.96);
            transition: 0.1s;
        }
        .btn-outline {
            background: var(--card-bg);
            color: var(--text);
            border: 1.5px solid var(--border);
        }
        .btn-outline:hover {
            border-color: var(--primary);
            color: var(--primary);
            background: var(--primary-light);
        }
        .btn-primary {
            background: var(--primary);
            color: #fff;
            box-shadow: 0 4px 14px rgba(232, 83, 108, 0.3);
        }
        .btn-primary:hover {
            background: var(--primary-dark);
            box-shadow: 0 6px 20px rgba(232, 83, 108, 0.4);
            transform: translateY(-1px);
        }
        .btn-accent {
            background: var(--accent);
            color: #fff;
            box-shadow: 0 4px 14px rgba(249, 166, 108, 0.3);
        }
        .btn-accent:hover {
            background: #e89150;
            box-shadow: 0 6px 20px rgba(249, 166, 108, 0.4);
            transform: translateY(-1px);
        }
        .btn-sm {
            padding: 6px 12px;
            font-size: 0.8rem;
            border-radius: 30px;
        }
        .btn-xs {
            padding: 4px 10px;
            font-size: 0.72rem;
            border-radius: 20px;
            gap: 3px;
        }

        /* ===== Main Layout ===== */
        .main-container {
            max-width: 1100px;
            margin: 0 auto;
            padding: 20px 20px 40px;
            display: grid;
            grid-template-columns: 360px 1fr;
            gap: 24px;
            align-items: start;
        }
        @media (max-width: 820px) {
            .main-container {
                grid-template-columns: 1fr;
                gap: 18px;
                padding: 14px 14px 100px;
            }
        }

        /* ===== Panel ===== */
        .panel {
            display: flex;
            flex-direction: column;
            gap: 16px;
            position: sticky;
            top: 90px;
        }
        @media (max-width: 820px) {
            .panel {
                position: static;
                top: auto;
                gap: 12px;
            }
        }
        .panel-card {
            background: var(--card-bg);
            border-radius: var(--radius-lg);
            padding: 20px 22px;
            box-shadow: var(--shadow);
            border: 1px solid var(--border);
            transition: var(--transition);
        }
        .panel-card:hover {
            box-shadow: var(--shadow-lg);
        }
        .panel-title {
            font-size: 1rem;
            font-weight: 700;
            margin-bottom: 14px;
            display: flex;
            align-items: center;
            gap: 7px;
            color: var(--text);
            letter-spacing: -0.2px;
        }
        .panel-title .icon {
            font-size: 1.2rem;
        }

        /* Form */
        .form-group {
            margin-bottom: 12px;
        }
        .form-group:last-child {
            margin-bottom: 0;
        }
        .form-label {
            display: block;
            font-size: 0.82rem;
            font-weight: 600;
            color: var(--text-light);
            margin-bottom: 5px;
            letter-spacing: 0.1px;
        }
        .form-input,
        .form-textarea {
            width: 100%;
            padding: 10px 14px;
            border: 1.5px solid var(--border);
            border-radius: var(--radius-sm);
            font-size: 0.9rem;
            font-family: var(--font);
            transition: var(--transition);
            background: #fefcfc;
            color: var(--text);
            resize: vertical;
        }
        .form-input:focus,
        .form-textarea:focus {
            outline: none;
            border-color: var(--primary);
            box-shadow: 0 0 0 4px rgba(232, 83, 108, 0.08);
            background: #fff;
        }
        .form-textarea {
            min-height: 60px;
            resize: vertical;
        }
        .form-row {
            display: flex;
            gap: 10px;
        }
        .form-row>* {
            flex: 1;
        }
        .tag-chips {
            display: flex;
            flex-wrap: wrap;
            gap: 6px;
        }
        .tag-chip {
            padding: 6px 13px;
            border-radius: 50px;
            font-size: 0.78rem;
            font-weight: 600;
            cursor: pointer;
            border: 1.5px solid var(--border);
            background: #fff;
            color: var(--text-light);
            transition: var(--transition);
            user-select: none;
            -webkit-tap-highlight-color: transparent;
            white-space: nowrap;
            letter-spacing: 0.2px;
        }
        .tag-chip:hover {
            border-color: var(--primary);
            background: var(--primary-light);
            color: var(--primary);
        }
        .tag-chip.selected {
            background: var(--primary);
            color: #fff;
            border-color: var(--primary);
            box-shadow: 0 2px 8px rgba(232, 83, 108, 0.25);
        }
        .tag-chip:active {
            transform: scale(0.94);
            transition: 0.1s;
        }

        /* Budget */
        .budget-chips {
            display: flex;
            flex-wrap: wrap;
            gap: 6px;
            margin-bottom: 10px;
        }
        .budget-chip {
            padding: 7px 14px;
            border-radius: 50px;
            font-size: 0.8rem;
            font-weight: 600;
            cursor: pointer;
            border: 1.5px solid var(--border);
            background: #fff;
            color: var(--text-light);
            transition: var(--transition);
            user-select: none;
            -webkit-tap-highlight-color: transparent;
            white-space: nowrap;
        }
        .budget-chip:hover {
            border-color: var(--accent);
            background: var(--accent-light);
            color: var(--accent);
        }
        .budget-chip.active {
            background: var(--accent);
            color: #fff;
            border-color: var(--accent);
            box-shadow: 0 2px 8px rgba(249, 166, 108, 0.3);
        }
        .budget-custom {
            display: flex;
            gap: 8px;
            align-items: center;
        }
        .budget-custom input {
            flex: 1;
            padding: 8px 12px;
            border: 1.5px solid var(--border);
            border-radius: var(--radius-sm);
            font-size: 0.85rem;
            font-family: var(--font);
            transition: var(--transition);
            background: #fefcfc;
        }
        .budget-custom input:focus {
            outline: none;
            border-color: var(--accent);
            box-shadow: 0 0 0 4px rgba(249, 166, 108, 0.08);
            background: #fff;
        }
        .budget-display {
            font-size: 0.85rem;
            color: var(--text-light);
            margin-top: 6px;
            font-weight: 500;
        }
        .budget-display strong {
            color: var(--accent);
            font-weight: 700;
        }

        /* ===== Content Area ===== */
        .content-area {
            display: flex;
            flex-direction: column;
            gap: 16px;
        }
        .toolbar {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            align-items: center;
            justify-content: space-between;
        }
        .toolbar-left {
            display: flex;
            flex-wrap: wrap;
            gap: 6px;
            align-items: center;
        }
        .filter-tag {
            padding: 5px 11px;
            border-radius: 50px;
            font-size: 0.75rem;
            font-weight: 600;
            cursor: pointer;
            border: 1.5px solid var(--border);
            background: #fff;
            color: var(--text-light);
            transition: var(--transition);
            user-select: none;
            -webkit-tap-highlight-color: transparent;
            white-space: nowrap;
        }
        .filter-tag:hover {
            border-color: var(--primary);
            color: var(--primary);
            background: #fff5f7;
        }
        .filter-tag.active {
            background: #fef0f2;
            color: var(--primary);
            border-color: var(--primary);
            font-weight: 700;
        }
        .result-count {
            font-size: 0.8rem;
            color: var(--text-muted);
            font-weight: 500;
        }

        /* Spots Grid */
        .spots-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
            gap: 14px;
        }
        @media (max-width: 500px) {
            .spots-grid {
                grid-template-columns: 1fr 1fr;
                gap: 10px;
            }
        }
        @media (max-width: 380px) {
            .spots-grid {
                grid-template-columns: 1fr;
            }
        }
        .spot-card {
            background: var(--card-bg);
            border-radius: var(--radius);
            padding: 16px 18px;
            box-shadow: var(--shadow);
            border: 1.5px solid transparent;
            transition: var(--transition);
            cursor: pointer;
            position: relative;
            display: flex;
            flex-direction: column;
            gap: 8px;
            user-select: none;
            -webkit-tap-highlight-color: transparent;
        }
        .spot-card:hover {
            border-color: #f0d0d5;
            box-shadow: var(--shadow-lg);
            transform: translateY(-2px);
        }
        .spot-card:active {
            transform: scale(0.97);
            transition: 0.1s;
        }
        .spot-card.visited {
            opacity: 0.55;
            background: #fafafa;
            border-color: #eee;
        }
        .spot-card.visited .spot-name {
            text-decoration: line-through;
            text-decoration-color: #ccc;
            text-decoration-thickness: 2px;
        }
        .spot-card.over-budget {
            border-color: #ffe0d0;
            background: #fffdfb;
        }
        .spot-card-header {
            display: flex;
            align-items: flex-start;
            justify-content: space-between;
            gap: 8px;
        }
        .spot-name {
            font-weight: 700;
            font-size: 1rem;
            color: var(--text);
            letter-spacing: -0.2px;
            word-break: break-word;
            line-height: 1.3;
        }
        .spot-cost {
            font-weight: 700;
            font-size: 0.85rem;
            padding: 3px 10px;
            border-radius: 50px;
            white-space: nowrap;
            flex-shrink: 0;
            letter-spacing: 0.3px;
        }
        .cost-free {
            background: var(--green-light);
            color: #2d7d4f;
        }
        .cost-low {
            background: #e3f2fd;
            color: #2563a0;
        }
        .cost-mid {
            background: var(--yellow-light);
            color: #8a6d20;
        }
        .cost-high {
            background: var(--orange-light);
            color: #a04030;
        }
        .cost-luxury {
            background: #fde8ec;
            color: #9b3050;
        }
        .spot-desc {
            font-size: 0.8rem;
            color: var(--text-light);
            line-height: 1.45;
            display: -webkit-box;
            -webkit-line-clamp: 2;
            -webkit-box-orient: vertical;
            overflow: hidden;
        }
        .spot-tags {
            display: flex;
            flex-wrap: wrap;
            gap: 4px;
        }
        .spot-tag {
            font-size: 0.7rem;
            padding: 2px 8px;
            border-radius: 30px;
            background: #f8f0f2;
            color: #8a6070;
            font-weight: 500;
            white-space: nowrap;
        }
        .spot-actions {
            display: flex;
            gap: 6px;
            margin-top: 2px;
        }
        .spot-actions .btn-xs {
            font-size: 0.7rem;
        }
        .over-budget-badge {
            position: absolute;
            top: -6px;
            right: -6px;
            background: #fff;
            border: 1.5px solid #f0c0b0;
            color: #c07050;
            font-size: 0.65rem;
            font-weight: 700;
            padding: 3px 8px;
            border-radius: 50px;
            white-space: nowrap;
            box-shadow: var(--shadow-sm);
            letter-spacing: 0.2px;
        }
        .visited-badge {
            position: absolute;
            top: -6px;
            left: -6px;
            background: #e0e0e0;
            color: #888;
            font-size: 0.65rem;
            font-weight: 700;
            padding: 3px 8px;
            border-radius: 50px;
            white-space: nowrap;
            box-shadow: var(--shadow-sm);
            letter-spacing: 0.2px;
        }

        /* Empty State */
        .empty-state {
            text-align: center;
            padding: 50px 20px;
            color: var(--text-muted);
        }
        .empty-state .emoji {
            font-size: 4rem;
            display: block;
            margin-bottom: 12px;
            animation: float 3s ease-in-out infinite;
        }
        @keyframes float {
            0%,
            100% {
                transform: translateY(0);
            }
            50% {
                transform: translateY(-14px);
            }
        }
        .empty-state p {
            font-size: 0.95rem;
            font-weight: 500;
        }

        /* ===== Random Button ===== */
        .random-section {
            display: flex;
            justify-content: center;
            padding: 10px 0 20px;
        }
        .btn-random {
            display: inline-flex;
            align-items: center;
            gap: 10px;
            padding: 16px 36px;
            font-size: 1.15rem;
            font-weight: 700;
            border-radius: 60px;
            cursor: pointer;
            border: none;
            font-family: var(--font);
            background: linear-gradient(135deg, #e8536c 0%, #f08060 50%, #f9a66c 100%);
            color: #fff;
            box-shadow: 0 8px 28px rgba(232, 83, 108, 0.35);
            transition: var(--transition);
            letter-spacing: 0.3px;
            user-select: none;
            -webkit-tap-highlight-color: transparent;
            position: relative;
            overflow: hidden;
        }
        .btn-random:hover {
            box-shadow: 0 12px 36px rgba(232, 83, 108, 0.45);
            transform: translateY(-3px);
        }
        .btn-random:active {
            transform: scale(0.94);
            transition: 0.1s;
            box-shadow: 0 4px 16px rgba(232, 83, 108, 0.3);
        }
        .btn-random::after {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(255, 255, 255, 0.2) 0%, transparent 60%);
            animation: shimmer 3s ease-in-out infinite;
        }
        @keyframes shimmer {
            0%,
            100% {
                transform: translate(0, 0);
            }
            50% {
                transform: translate(10%, -10%);
            }
        }
        .btn-random .dice {
            font-size: 1.5rem;
