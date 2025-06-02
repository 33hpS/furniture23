<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Furniture Orders Tracker</title>
    <style>
        :root {
            --primary-color: #2563eb;
            --primary-dark: #1e40af;
            --secondary-color: #059669;
            --danger-color: #dc2626;
            --warning-color: #d97706;
            --info-color: #0891b2;
            --surface-color: #ffffff;
            --background-color: #f8fafc;
            --text-primary: #1f2937;
            --text-secondary: #6b7280;
            --border-color: #d1d5db;
            --shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1);
            --shadow-lg: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
            --transition: all 0.2s ease-in-out;
            --painted-color: #dbeafe;
            --film-color: #f3e8ff;
        }

        [data-theme="dark"] {
            --surface-color: #1f2937;
            --background-color: #111827;
            --text-primary: #f9fafb;
            --text-secondary: #9ca3af;
            --border-color: #374151;
            --painted-color: #1e3a8a;
            --film-color: #581c87;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', system-ui, sans-serif;
            background: var(--background-color);
            color: var(--text-primary);
            line-height: 1.5;
            transition: var(--transition);
        }

        .app-container {
            min-height: 100vh;
            display: flex;
            flex-direction: column;
        }

        /* Header */
        .header {
            background: var(--surface-color);
            color: var(--text-primary);
            padding: 1rem 2rem;
            box-shadow: var(--shadow-lg);
            position: sticky;
            top: 0;
            z-index: 100;
            border-bottom: 2px solid var(--border-color);
        }

        .header-content {
            max-width: 1400px;
            margin: 0 auto;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 1rem;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 1rem;
            font-size: 1.25rem;
            font-weight: 700;
            color: var(--primary-color);
        }

        .header-controls {
            display: flex;
            align-items: center;
            gap: 1rem;
            flex-wrap: wrap;
        }

        .language-selector {
            display: flex;
            background: var(--background-color);
            border: 1px solid var(--border-color);
            border-radius: 0.375rem;
            overflow: hidden;
        }

        .lang-btn {
            background: transparent;
            border: none;
            color: var(--text-secondary);
            padding: 0.5rem 1rem;
            cursor: pointer;
            transition: var(--transition);
            font-size: 0.875rem;
            font-weight: 500;
            border-right: 1px solid var(--border-color);
        }

        .lang-btn:last-child {
            border-right: none;
        }

        .lang-btn.active {
            background: var(--primary-color);
            color: white;
        }

        .lang-btn:hover:not(.active) {
            background: var(--background-color);
        }

        .theme-toggle {
            background: var(--background-color);
            border: 1px solid var(--border-color);
            color: var(--text-primary);
            padding: 0.5rem;
            border-radius: 0.375rem;
            cursor: pointer;
            transition: var(--transition);
            font-size: 1rem;
        }

        .theme-toggle:hover {
            background: var(--border-color);
        }

        .user-info {
            display: flex;
            align-items: center;
            gap: 0.75rem;
        }

        .user-role {
            background: var(--background-color);
            padding: 0.5rem 1rem;
            border-radius: 0.375rem;
            font-size: 0.875rem;
            border: 1px solid var(--border-color);
            font-weight: 500;
        }

        /* Main Content */
        .main-content {
            flex: 1;
            max-width: 1400px;
            margin: 0 auto;
            padding: 2rem;
            width: 100%;
        }

        /* Controls Panel */
        .controls-panel {
            background: var(--surface-color);
            border-radius: 0.5rem;
            padding: 1.5rem;
            margin-bottom: 2rem;
            box-shadow: var(--shadow);
            border: 1px solid var(--border-color);
        }

        .controls-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 1rem;
            align-items: center;
        }

        .btn {
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
            padding: 0.75rem 1rem;
            border: 1px solid var(--border-color);
            border-radius: 0.375rem;
            font-weight: 500;
            font-size: 0.875rem;
            cursor: pointer;
            transition: var(--transition);
            text-decoration: none;
            justify-content: center;
            background: var(--surface-color);
            color: var(--text-primary);
        }

        .btn:hover {
            background: var(--background-color);
        }

        .btn-primary {
            background: var(--primary-color);
            color: white;
            border-color: var(--primary-color);
        }

        .btn-primary:hover {
            background: var(--primary-dark);
            border-color: var(--primary-dark);
        }

        .btn-success {
            background: var(--secondary-color);
            color: white;
            border-color: var(--secondary-color);
        }

        .btn-warning {
            background: var(--warning-color);
            color: white;
            border-color: var(--warning-color);
        }

        .btn-info {
            background: var(--info-color);
            color: white;
            border-color: var(--info-color);
        }

        .btn-danger {
            background: var(--danger-color);
            color: white;
            border-color: var(--danger-color);
        }

        .btn-secondary {
            background: var(--text-secondary);
            color: white;
            border-color: var(--text-secondary);
        }

        .input-field {
            padding: 0.75rem;
            border: 1px solid var(--border-color);
            border-radius: 0.375rem;
            background: var(--surface-color);
            color: var(--text-primary);
            font-size: 0.875rem;
            transition: var(--transition);
            width: 100%;
        }

        .input-field:focus {
            outline: none;
            border-color: var(--primary-color);
            box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.1);
        }

        /* Pagination */
        .pagination-container {
            background: var(--surface-color);
            border-radius: 0.5rem;
            padding: 1rem;
            margin-bottom: 1rem;
            box-shadow: var(--shadow);
            border: 1px solid var(--border-color);
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 1rem;
        }

        .month-selector {
            display: flex;
            align-items: center;
            gap: 1rem;
        }

        .month-nav {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            position: relative;
            z-index: 2;
        }

        .month-nav button {
            background: var(--background-color);
            border: 1px solid var(--border-color);
            padding: 0.5rem;
            border-radius: 0.375rem;
            cursor: pointer;
            transition: var(--transition);
        }

        .month-nav button:hover {
            background: var(--border-color);
        }

        .current-month {
            font-weight: 600;
            font-size: 1.125rem;
            min-width: 200px;
            text-align: center;
        }

        .orders-count {
            font-size: 0.875rem;
            color: var(--text-secondary);
        }

        /* Statistics Panel */
        .statistics-panel {
            background: var(--surface-color);
            border-radius: 0.5rem;
            padding: 1.5rem;
            margin-bottom: 2rem;
            box-shadow: var(--shadow);
            border: 1px solid var(--border-color);
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 1rem;
        }

        .stat-card {
            background: var(--background-color);
            border: 1px solid var(--border-color);
            border-radius: 0.375rem;
            padding: 1rem;
            display: flex;
            align-items: center;
            gap: 1rem;
            transition: var(--transition);
            position: relative;
        }

        .stat-card:hover {
            border-color: var(--primary-color);
        }

        .stat-card.clickable {
            cursor: pointer;
        }

        .stat-card.clickable:hover {
            transform: translateY(-2px);
            box-shadow: var(--shadow-lg);
        }

        .stat-icon {
            font-size: 2rem;
            flex-shrink: 0;
        }

        .stat-content {
            flex: 1;
        }

        .stat-value {
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--primary-color);
            line-height: 1;
        }

        .stat-label {
            font-size: 0.875rem;
            color: var(--text-secondary);
            margin-top: 0.25rem;
        }

        /* Month animations */
        .month-selector {
            display: flex;
            align-items: center;
            gap: 1rem;
            position: relative;
            overflow: hidden;
            min-height: 60px;
        }

        .month-animation {
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            pointer-events: none;
            z-index: 1;
        }

        /* January - Snow */
        .month-animation.january::before {
            content: '❄️ ❄️ ❄️';
            position: absolute;
            top: -20px;
            left: 0;
            right: 0;
            animation: snowfall 3s linear infinite;
            opacity: 0.7;
        }

        @keyframes snowfall {
            0% { transform: translateY(-20px); opacity: 0; }
            50% { opacity: 1; }
            100% { transform: translateY(100px); opacity: 0; }
        }

        /* February - Hearts */
        .month-animation.february::before {
            content: '💕 💖 💝';
            position: absolute;
            animation: floating-hearts 2s ease-in-out infinite;
            opacity: 0.8;
        }

        @keyframes floating-hearts {
            0%, 100% { transform: translateY(0) rotate(0deg); }
            50% { transform: translateY(-10px) rotate(5deg); }
        }

        /* March - Flowers */
        .month-animation.march::before {
            content: '🌸 🌺 🌷';
            position: absolute;
            animation: blooming 2.5s ease-in-out infinite;
            opacity: 0.8;
        }

        @keyframes blooming {
            0%, 100% { transform: scale(1) rotate(0deg); }
            50% { transform: scale(1.1) rotate(2deg); }
        }

        /* April - Rain */
        .month-animation.april::before {
            content: '🌧️ ☔ 💧';
            position: absolute;
            animation: rainfall 2s linear infinite;
            opacity: 0.7;
        }

        @keyframes rainfall {
            0% { transform: translateY(-10px); }
            100% { transform: translateY(40px); }
        }

        /* May - Leaves */
        .month-animation.may::before {
            content: '🍃 🌿 🌱';
            position: absolute;
            animation: leaf-dance 3s ease-in-out infinite;
            opacity: 0.8;
        }

        @keyframes leaf-dance {
            0%, 100% { transform: translateX(0) rotate(0deg); }
            25% { transform: translateX(5px) rotate(5deg); }
            75% { transform: translateX(-5px) rotate(-5deg); }
        }

        /* June - Sun */
        .month-animation.june::before {
            content: '☀️ 🌞 ✨';
            position: absolute;
            animation: sunshine 2s ease-in-out infinite;
            opacity: 0.9;
        }

        @keyframes sunshine {
            0%, 100% { transform: scale(1) rotate(0deg); }
            50% { transform: scale(1.05) rotate(10deg); }
        }

        /* July - Fire/Heat */
        .month-animation.july::before {
            content: '🔥 🌡️ ☀️';
            position: absolute;
            animation: heat-wave 1.5s ease-in-out infinite;
            opacity: 0.8;
        }

        @keyframes heat-wave {
            0%, 100% { transform: translateY(0) scale(1); }
            50% { transform: translateY(-3px) scale(1.02); }
        }

        /* August - Vacation */
        .month-animation.august::before {
            content: '🏖️ 🌊 🏄';
            position: absolute;
            animation: wave-motion 2.5s ease-in-out infinite;
            opacity: 0.8;
        }

        @keyframes wave-motion {
            0%, 100% { transform: translateX(0) rotate(0deg); }
            33% { transform: translateX(3px) rotate(1deg); }
            66% { transform: translateX(-3px) rotate(-1deg); }
        }

        /* September - Autumn */
        .month-animation.september::before {
            content: '🍂 🍁 🌾';
            position: absolute;
            animation: autumn-fall 3s ease-in-out infinite;
            opacity: 0.8;
        }

        @keyframes autumn-fall {
            0% { transform: translateY(-10px) rotate(0deg); opacity: 0; }
            50% { opacity: 1; }
            100% { transform: translateY(30px) rotate(180deg); opacity: 0; }
        }

        /* October - Halloween */
        .month-animation.october::before {
            content: '🎃 👻 🦇';
            position: absolute;
            animation: spooky-float 2s ease-in-out infinite;
            opacity: 0.8;
        }

        @keyframes spooky-float {
            0%, 100% { transform: translateY(0) rotate(0deg); }
            50% { transform: translateY(-8px) rotate(3deg); }
        }

        /* November - Wind */
        .month-animation.november::before {
            content: '🌬️ 🍃 💨';
            position: absolute;
            animation: windy 2s linear infinite;
            opacity: 0.7;
        }

        @keyframes windy {
            0% { transform: translateX(-20px); }
            100% { transform: translateX(50px); }
        }

        /* December - Winter/Christmas */
        .month-animation.december::before {
            content: '🎄 ❄️ 🎅';
            position: absolute;
            animation: festive 2.5s ease-in-out infinite;
            opacity: 0.8;
        }

        @keyframes festive {
            0%, 100% { transform: scale(1) rotate(0deg); }
            25% { transform: scale(1.05) rotate(1deg); }
            75% { transform: scale(1.02) rotate(-1deg); }
        }

        /* Orders Table */
        .table-container {
            background: var(--surface-color);
            border-radius: 0.5rem;
            overflow: hidden;
            box-shadow: var(--shadow);
            border: 1px solid var(--border-color);
        }

        .table-wrapper {
            overflow-x: auto;
            /* Removed max-height to eliminate scrolling */
        }

        .orders-table {
            width: 100%;
            border-collapse: collapse;
            font-size: 0.875rem;
        }

        .orders-table th {
            background: var(--background-color);
            color: var(--text-primary);
            padding: 1rem 0.75rem;
            text-align: center;
            font-weight: 600;
            position: sticky;
            top: 0;
            z-index: 10;
            border-bottom: 2px solid var(--border-color);
        }

        .orders-table td {
            padding: 1rem 0.75rem;
            text-align: center;
            border-bottom: 1px solid var(--border-color);
            transition: var(--transition);
        }

        .orders-table tr:hover {
            background: var(--background-color);
        }

        .orders-table tr.problem-order {
            background: rgba(220, 38, 38, 0.1);
        }

        .orders-table tr.painted-order {
            background: var(--painted-color);
        }

        .orders-table tr.film-order {
            background: var(--film-color);
        }

        .order-number {
            font-weight: 600;
            color: var(--primary-color);
            cursor: pointer;
            transition: var(--transition);
            padding: 0.25rem;
            border-radius: 0.25rem;
        }

        .order-number:hover {
            background: rgba(37, 99, 235, 0.1);
        }

        .order-meta {
            font-size: 0.75rem;
            color: var(--text-secondary);
            margin-top: 0.25rem;
        }

        .priority-badge {
            padding: 0.25rem 0.75rem;
            border-radius: 0.25rem;
            font-size: 0.75rem;
            font-weight: 500;
            border: 1px solid;
        }

        .priority-high {
            background: rgba(220, 38, 38, 0.1);
            color: var(--danger-color);
            border-color: var(--danger-color);
        }

        .priority-medium {
            background: rgba(217, 119, 6, 0.1);
            color: var(--warning-color);
            border-color: var(--warning-color);
        }

        .priority-low {
            background: rgba(5, 150, 105, 0.1);
            color: var(--secondary-color);
            border-color: var(--secondary-color);
        }

        .status-indicator {
            width: 2.5rem;
            height: 2.5rem;
            border-radius: 0.25rem;
            border: 2px solid var(--border-color);
            background: var(--surface-color);
            cursor: pointer;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            margin: 0 auto;
            font-size: 1rem;
            transition: var(--transition);
            position: relative;
        }

        .status-indicator:hover {
            border-color: var(--primary-color);
        }

        .status-indicator.disabled {
            opacity: 0.3;
            cursor: not-allowed;
            background: var(--background-color);
        }

        .status-pending {
            border-color: var(--border-color);
            color: var(--text-secondary);
        }

        .status-completed {
            background: var(--secondary-color);
            border-color: var(--secondary-color);
            color: white;
        }

        .status-problem {
            background: var(--danger-color);
            border-color: var(--danger-color);
            color: white;
        }

        .status-time {
            font-size: 0.625rem;
            color: var(--text-secondary);
            text-align: center;
            margin-top: 0.25rem;
            line-height: 1;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
            max-width: 100%;
        }

        .status-completed .status-time,
        .status-problem .status-time {
            color: rgba(255, 255, 255, 0.8);
        }

        .stage-cell {
            padding: 0.5rem 0.25rem;
            vertical-align: top;
        }

        /* Type badges */
        .type-badge {
            padding: 0.25rem 0.75rem;
            border-radius: 0.25rem;
            font-size: 0.75rem;
            font-weight: 500;
            border: 1px solid;
        }

        .type-painted {
            background: rgba(37, 99, 235, 0.1);
            color: var(--primary-color);
            border-color: var(--primary-color);
        }

        .type-film {
            background: rgba(139, 92, 246, 0.1);
            color: #8b5cf6;
            border-color: #8b5cf6;
        }

        /* Modal Styles */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            z-index: 1000;
        }

        .modal-content {
            background: var(--surface-color);
            margin: 2rem auto;
            padding: 2rem;
            border-radius: 0.5rem;
            width: 90%;
            max-width: 600px;
            max-height: 90vh;
            overflow-y: auto;
            box-shadow: var(--shadow-lg);
            border: 1px solid var(--border-color);
        }

        .modal-large {
            max-width: 1000px;
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 2rem;
            padding-bottom: 1rem;
            border-bottom: 1px solid var(--border-color);
        }

        .modal-title {
            font-size: 1.25rem;
            font-weight: 600;
            color: var(--text-primary);
        }

        .close-btn {
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: var(--text-secondary);
            padding: 0.25rem;
            border-radius: 0.25rem;
            transition: var(--transition);
        }

        .close-btn:hover {
            background: var(--background-color);
        }

        /* Wizard Steps */
        .wizard-container {
            margin-bottom: 2rem;
        }

        .wizard-steps {
            display: flex;
            justify-content: space-between;
            margin-bottom: 2rem;
            position: relative;
        }

        .wizard-steps::before {
            content: '';
            position: absolute;
            top: 1.5rem;
            left: 2rem;
            right: 2rem;
            height: 2px;
            background: var(--border-color);
            z-index: 1;
        }

        .wizard-step {
            display: flex;
            flex-direction: column;
            align-items: center;
            text-align: center;
            position: relative;
            z-index: 2;
            flex: 1;
        }

        .step-circle {
            width: 3rem;
            height: 3rem;
            border-radius: 50%;
            background: var(--background-color);
            color: var(--text-secondary);
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: 600;
            margin-bottom: 0.5rem;
            transition: var(--transition);
            border: 2px solid var(--border-color);
        }

        .step-circle.active {
            background: var(--primary-color);
            color: white;
            border-color: var(--primary-color);
        }

        .step-circle.completed {
            background: var(--secondary-color);
            color: white;
            border-color: var(--secondary-color);
        }

        .step-label {
            font-size: 0.75rem;
            color: var(--text-secondary);
            font-weight: 500;
        }

        .step-content {
            display: none;
        }

        .step-content.active {
            display: block;
        }

        /* Form Styles */
        .form-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 1.5rem;
        }

        .form-group {
            margin-bottom: 1.5rem;
        }

        .form-label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 500;
            color: var(--text-primary);
            font-size: 0.875rem;
        }

        .form-input {
            width: 100%;
            padding: 0.75rem;
            border: 1px solid var(--border-color);
            border-radius: 0.375rem;
            background: var(--surface-color);
            color: var(--text-primary);
            transition: var(--transition);
        }

        .form-input:focus {
            outline: none;
            border-color: var(--primary-color);
            box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.1);
        }

        .form-textarea {
            min-height: 100px;
            resize: vertical;
        }

        /* Tech Card Upload */
        .tech-card-section {
            background: var(--background-color);
            border: 1px solid var(--border-color);
            border-radius: 0.5rem;
            padding: 1.5rem;
            margin-top: 1rem;
        }

        .tech-card-upload {
            border: 2px dashed var(--border-color);
            border-radius: 0.375rem;
            padding: 2rem;
            text-align: center;
            cursor: pointer;
            transition: var(--transition);
            margin-bottom: 1rem;
        }

        .tech-card-upload:hover,
        .tech-card-upload.dragover {
            border-color: var(--primary-color);
            background: rgba(37, 99, 235, 0.05);
        }

        .material-consumption {
            background: var(--surface-color);
            border: 1px solid var(--border-color);
            border-radius: 0.375rem;
            padding: 1rem;
            margin-top: 1rem;
        }

        .material-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0.75rem;
            border-bottom: 1px solid var(--border-color);
        }

        .material-item:last-child {
            border-bottom: none;
        }

        /* Notifications */
        .notification {
            position: fixed;
            top: 2rem;
            right: 2rem;
            background: var(--secondary-color);
            color: white;
            padding: 1rem 1.5rem;
            border-radius: 0.375rem;
            box-shadow: var(--shadow-lg);
            z-index: 1001;
            transform: translateX(400px);
            transition: var(--transition);
            display: flex;
            align-items: center;
            gap: 0.5rem;
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        .notification.show {
            transform: translateX(0);
        }

        .notification.error {
            background: var(--danger-color);
        }

        .notification.warning {
            background: var(--warning-color);
        }

        /* Responsive Design */
        @media (max-width: 768px) {
            .main-content {
                padding: 1rem;
            }

            .header-content {
                flex-direction: column;
                gap: 1rem;
            }

            .controls-grid {
                grid-template-columns: 1fr;
            }

            .stats-grid {
                grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            }

            .stat-card {
                padding: 0.75rem;
                gap: 0.75rem;
            }

            .stat-icon {
                font-size: 1.5rem;
            }

            .stat-value {
                font-size: 1.25rem;
            }

            .orders-table {
                font-size: 0.75rem;
            }

            .status-indicator {
                width: 2rem;
                height: 2rem;
                font-size: 0.875rem;
            }

            .status-time {
                font-size: 0.5rem;
            }

            .wizard-steps {
                flex-direction: column;
                gap: 1rem;
            }

            .wizard-steps::before {
                display: none;
            }

            .pagination-container {
                flex-direction: column;
                text-align: center;
            }
        }

        /* Custom scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }

        ::-webkit-scrollbar-track {
            background: var(--background-color);
        }

        ::-webkit-scrollbar-thumb {
            background: var(--border-color);
            border-radius: 4px;
        }

        ::-webkit-scrollbar-thumb:hover {
            background: var(--text-secondary);
        }
    </style>
</head>
<body>
    <div class="app-container">
        <!-- Header -->
        <header class="header">
            <div class="header-content">
                <div class="logo">
                    <span>🏭</span>
                    <span data-translate="app_title">Furniture Orders Tracker</span>
                </div>
                <div class="header-controls">
                    <div class="language-selector">
                        <button class="lang-btn active" onclick="setLanguage('en')" data-lang="en">EN</button>
                        <button class="lang-btn" onclick="setLanguage('ru')" data-lang="ru">RU</button>
                        <button class="lang-btn" onclick="setLanguage('ky')" data-lang="ky">KY</button>
                    </div>
                    <button class="theme-toggle" onclick="toggleTheme()">
                        <span id="themeIcon">🌙</span>
                    </button>
                    <div class="user-info">
                        <span id="userName">Ivan Petrov</span>
                        <span class="user-role" id="userRole" data-translate="role_worker">Worker</span>
                    </div>
                    <button class="btn btn-danger" onclick="logout()" data-translate="logout">Logout</button>
                </div>
            </div>
        </header>

        <!-- Main Content -->
        <main class="main-content">
            <!-- Controls Panel -->
            <div class="controls-panel">
                <div class="controls-grid">
                    <button class="btn btn-primary" id="newOrderBtn" onclick="showOrderWizard()">
                        ➕ <span data-translate="new_order">New Order</span>
                    </button>
                    <button class="btn btn-success" id="statsBtn" onclick="showStats()">
                        📊 <span data-translate="statistics">Statistics</span>
                    </button>
                    <button class="btn btn-warning" onclick="exportData()">
                        📤 <span data-translate="export">Export</span>
                    </button>
                    <button class="btn btn-info" onclick="importData()">
                        📥 <span data-translate="import">Import</span>
                    </button>
                    <input type="text" class="input-field" data-translate-placeholder="search_orders" placeholder="🔍 Search orders..." 
                           id="searchBox" onkeyup="searchOrders()">
                    <select class="input-field" id="filterPriority" onchange="filterOrders()">
                        <option value="" data-translate="all_priorities">All Priorities</option>
                        <option value="high" data-translate="high">High</option>
                        <option value="medium" data-translate="medium">Medium</option>
                        <option value="low" data-translate="low">Low</option>
                    </select>
                    <select class="input-field" id="filterStatus" onchange="filterOrders()">
                        <option value="" data-translate="all_statuses">All Statuses</option>
                        <option value="active" data-translate="in_progress">In Progress</option>
                        <option value="completed" data-translate="completed">Completed</option>
                        <option value="problems" data-translate="with_problems">With Problems</option>
                    </select>
                    <select class="input-field" id="filterType" onchange="filterOrders()">
                        <option value="" data-translate="all_types">All Types</option>
                        <option value="painted" data-translate="painted">Painted</option>
                        <option value="film" data-translate="film">Film</option>
                    </select>
                </div>
            </div>

            <!-- Pagination Controls -->
            <div class="pagination-container">
                <div class="month-selector">
                    <div class="month-animation" id="monthAnimation"></div>
                    <div class="month-nav">
                        <button onclick="previousMonth()">‹</button>
                        <div class="current-month" id="currentMonth">January 2024</div>
                        <button onclick="nextMonth()">›</button>
                    </div>
                </div>
                <div class="orders-count" id="ordersCount">0 orders</div>
            </div>

            <!-- Monthly Statistics -->
            <div class="statistics-panel">
                <div class="stats-grid">
                    <div class="stat-card">
                        <div class="stat-icon">🎨</div>
                        <div class="stat-content">
                            <div class="stat-value" id="paintedCount">0</div>
                            <div class="stat-label" data-translate="painted_orders">Painted Orders</div>
                        </div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-icon">📄</div>
                        <div class="stat-content">
                            <div class="stat-value" id="filmCount">0</div>
                            <div class="stat-label" data-translate="film_orders">Film Orders</div>
                        </div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-icon">💰</div>
                        <div class="stat-content">
                            <div class="stat-value" id="totalRevenue">0₽</div>
                            <div class="stat-label" data-translate="total_revenue">Total Revenue</div>
                        </div>
                    </div>
                    <div class="stat-card clickable" onclick="showMaterialsDetails()">
                        <div class="stat-icon">📦</div>
                        <div class="stat-content">
                            <div class="stat-value" id="materialCost">0₽</div>
                            <div class="stat-label" data-translate="material_costs">Material Costs</div>
                        </div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-icon">✅</div>
                        <div class="stat-content">
                            <div class="stat-value" id="completedCount">0</div>
                            <div class="stat-label" data-translate="completed_orders">Completed Orders</div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Orders Table -->
            <div class="table-container">
                <div class="table-wrapper">
                    <table class="orders-table" id="ordersTable">
                        <thead>
                            <tr>
                                <th data-translate="order">Order</th>
                                <th data-translate="client">Client</th>
                                <th data-translate="name">Name</th>
                                <th data-translate="quantity">Qty</th>
                                <th data-translate="deadline">Deadline</th>
                                <th data-translate="cost">Cost</th>
                                <th data-translate="priority">Priority</th>
                                <th data-translate="type">Type</th>
                                <th data-translate="category">Category</th>
                                <th data-translate="new">New</th>
                                <th data-translate="cutting">Cutting</th>
                                <th data-translate="edging">Edging</th>
                                <th data-translate="cnc">CNC</th>
                                <th data-translate="sanding">Sanding</th>
                                <th data-translate="priming">Priming</th>
                                <th data-translate="painting">Painting</th>
                                <th data-translate="filming">Filming</th>
                                <th data-translate="drilling">Drilling</th>
                                <th data-translate="assembly">Assembly</th>
                                <th data-translate="quality">Quality</th>
                                <th data-translate="packing">Packing</th>
                                <th data-translate="ready">Ready</th>
                            </tr>
                        </thead>
                        <tbody id="ordersTableBody">
                            <!-- Orders will be rendered here -->
                        </tbody>
                    </table>
                </div>
            </div>
        </main>
    </div>

    <!-- Order Creation Wizard -->
    <div id="orderWizard" class="modal">
        <div class="modal-content modal-large">
            <div class="modal-header">
                <h2 class="modal-title" data-translate="order_wizard">Order Creation Wizard</h2>
                <button class="close-btn" onclick="closeOrderWizard()">&times;</button>
            </div>

            <div class="wizard-container">
                <div class="wizard-steps">
                    <div class="wizard-step">
                        <div class="step-circle active" id="step1Circle">1</div>
                        <div class="step-label" data-translate="basic_info">Basic Information</div>
                    </div>
                    <div class="wizard-step">
                        <div class="step-circle" id="step2Circle">2</div>
                        <div class="step-label" data-translate="materials">Materials</div>
                    </div>
                    <div class="wizard-step">
                        <div class="step-circle" id="step3Circle">3</div>
                        <div class="step-label" data-translate="tech_card">Tech Card</div>
                    </div>
                    <div class="wizard-step">
                        <div class="step-circle" id="step4Circle">4</div>
                        <div class="step-label" data-translate="files_dates">Files & Dates</div>
                    </div>
                    <div class="wizard-step">
                        <div class="step-circle" id="step5Circle">5</div>
                        <div class="step-label" data-translate="confirmation">Confirmation</div>
                    </div>
                </div>

                <!-- Step 1: Basic Information -->
                <div class="step-content active" id="step1">
                    <h3>📋 <span data-translate="basic_info">Basic Information</span></h3>
                    <div class="form-grid">
                        <div class="form-group">
                            <label class="form-label" data-translate="order_number">Order Number</label>
                            <input type="text" class="form-input" id="orderNumber" required>
                        </div>
                        <div class="form-group">
                            <label class="form-label" data-translate="client">Client</label>
                            <select class="form-input" id="clientName" required>
                                <option value="" data-translate="select_client">Select Client</option>
                                <option value="WASSER">WASSER</option>
                                <option value="custom" data-translate="custom_order">Custom Order</option>
                            </select>
                            <input type="text" class="form-input" id="customClientName" placeholder="Enter client name" style="display: none; margin-top: 0.5rem;">
                        </div>
                        <div class="form-group">
                            <label class="form-label" data-translate="product_name">Product Name</label>
                            <input type="text" class="form-input" id="orderName" required>
                        </div>
                        <div class="form-group">
                            <label class="form-label" data-translate="quantity_units">Quantity</label>
                            <input type="number" class="form-input" id="orderQuantity" min="1" required>
                        </div>
                        <div class="form-group">
                            <label class="form-label" data-translate="priority">Priority</label>
                            <select class="form-input" id="orderPriority" required>
                                <option value="low">🟢 <span data-translate="low">Low</span></option>
                                <option value="medium" selected>🟡 <span data-translate="medium">Medium</span></option>
                                <option value="high">🔴 <span data-translate="high">High</span></option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label class="form-label" data-translate="coating_type">Coating Type</label>
                            <select class="form-input" id="orderType" required onchange="updateTypeRestrictions()">
                                <option value="" data-translate="select_type">Select Type</option>
                                <option value="painted">🎨 <span data-translate="painted">Painted</span></option>
                                <option value="film">📄 <span data-translate="film">Film</span></option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label class="form-label" data-translate="product_category">Product Category</label>
                            <select class="form-input" id="orderCategory" required>
                                <option value="" data-translate="select_category">Select Category</option>
                                <option value="mirror">🪞 <span data-translate="mirror">Mirror</span></option>
                                <option value="cabinet">📦 <span data-translate="cabinet">Cabinet</span></option>
                                <option value="nightstand">🪑 <span data-translate="nightstand">Nightstand</span></option>
                                <option value="led">💡 <span data-translate="led">LED</span></option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label class="form-label" data-translate="order_cost">Order Cost (₽)</label>
                            <input type="number" class="form-input" id="orderCost" min="0" step="100">
                        </div>
                    </div>
                    <div class="form-group">
                        <label class="form-label" data-translate="order_description">Order Description</label>
                        <textarea class="form-input form-textarea" id="orderDescription" 
                                  data-translate-placeholder="description_placeholder" placeholder="Detailed product description, special requirements..."></textarea>
                    </div>
                </div>

                <!-- Step 2: Materials -->
                <div class="step-content" id="step2">
                    <h3>📦 <span data-translate="materials_selection">Materials Selection</span></h3>
                    <div class="materials-catalog" id="materialsCatalog">
                        <!-- Materials will be loaded here -->
                    </div>
                    <h4>✅ <span data-translate="selected_materials">Selected Materials:</span></h4>
                    <div id="selectedMaterials" style="min-height: 100px; border: 2px dashed var(--border-color); border-radius: 0.375rem; padding: 1rem; margin-top: 1rem;">
                        <p style="color: var(--text-secondary); text-align: center;" data-translate="no_materials">No materials selected</p>
                    </div>
                </div>

                <!-- Step 3: Tech Card -->
                <div class="step-content" id="step3">
                    <h3>📋 <span data-translate="tech_card">Tech Card Upload</span></h3>
                    <div class="tech-card-section">
                        <div class="tech-card-upload" id="techCardUpload" onclick="document.getElementById('techCardInput').click()">
                            <div style="font-size: 3rem; margin-bottom: 1rem;">📋</div>
                            <div style="font-weight: 600; margin-bottom: 0.5rem;" data-translate="upload_tech_card">Upload Tech Card</div>
                            <div style="color: var(--text-secondary); font-size: 0.875rem;" data-translate="tech_card_hint">CSV, Excel files with material consumption data</div>
                        </div>
                        <input type="file" id="techCardInput" accept=".csv,.xlsx,.xls" style="display: none;" onchange="handleTechCardUpload(event)">
                        
                        <div id="techCardResults" style="display: none;">
                            <h4 data-translate="parsed_materials">Parsed Materials:</h4>
                            <div class="material-consumption" id="parsedMaterials">
                                <!-- Parsed materials will appear here -->
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Step 4: Files and Deadlines -->
                <div class="step-content" id="step4">
                    <h3>📁 <span data-translate="files_dates">Files and Dates</span></h3>
                    <div class="form-grid">
                        <div class="form-group">
                            <label class="form-label" data-translate="start_date">Planned Start Date</label>
                            <input type="date" class="form-input" id="orderStartDate">
                        </div>
                        <div class="form-group">
                            <label class="form-label" data-translate="deadline_date">Desired Completion Date</label>
                            <input type="date" class="form-input" id="orderDeadline">
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label class="form-label" data-translate="file_upload">File Upload</label>
                        <div class="tech-card-upload" id="fileUploadArea" onclick="document.getElementById('fileInput').click()">
                            <div style="font-size: 3rem; margin-bottom: 1rem;">📁</div>
                            <div style="font-weight: 600; margin-bottom: 0.5rem;" data-translate="drag_files">Drag files here or click to select</div>
                            <div style="color: var(--text-secondary); font-size: 0.875rem;" data-translate="file_hint">Drawings, photos, tech cards (up to 10 MB each)</div>
                        </div>
                        <input type="file" id="fileInput" multiple accept=".pdf,.jpg,.jpeg,.png,.dwg,.doc,.docx" style="display: none;">
                        <div id="filesList"></div>
                    </div>
                </div>

                <!-- Step 5: Confirmation -->
                <div class="step-content" id="step5">
                    <h3>✅ <span data-translate="order_confirmation">Order Confirmation</span></h3>
                    <div id="orderSummary">
                        <!-- Order summary will be generated here -->
                    </div>
                </div>
            </div>

            <div style="display: flex; justify-content: space-between; margin-top: 2rem;">
                <button class="btn btn-secondary" id="prevBtn" onclick="previousStep()" style="display: none;">
                    ← <span data-translate="back">Back</span>
                </button>
                <div style="flex: 1;"></div>
                <button class="btn btn-primary" id="nextBtn" onclick="nextStep()">
                    <span data-translate="next">Next</span> →
                </button>
                <button class="btn btn-success" id="createBtn" onclick="createOrder()" style="display: none;">
                    ✅ <span data-translate="create_order">Create Order</span>
                </button>
            </div>
        </div>
    </div>

    <!-- Materials Details Modal -->
    <div id="materialsModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3 class="modal-title">📦 <span data-translate="materials_breakdown">Materials Breakdown</span></h3>
                <button class="close-btn" onclick="closeMaterialsModal()">&times;</button>
            </div>
            <div id="materialsBreakdown">
                <!-- Materials breakdown will be loaded here -->
            </div>
        </div>
    </div>

    <!-- Problem Modal -->
    <div id="problemModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3 class="modal-title">⚠️ <span data-translate="mark_problem">Mark Problem</span></h3>
                <button class="close-btn" onclick="closeProblemModal()">&times;</button>
            </div>
            <div class="form-group">
                <label class="form-label" data-translate="problem_description">Describe the problem:</label>
                <textarea class="form-input form-textarea" id="problemComment" 
                          data-translate-placeholder="problem_placeholder" placeholder="For example: no material, machine broken, waiting for drawings..."></textarea>
            </div>
            <div style="display: flex; gap: 1rem; justify-content: flex-end;">
                <button class="btn btn-secondary" onclick="closeProblemModal()" data-translate="cancel">Cancel</button>
                <button class="btn btn-danger" onclick="confirmProblem()" data-translate="mark_problem">Mark Problem</button>
            </div>
        </div>
    </div>

    <!-- Notification -->
    <div id="notification" class="notification"></div>

    <!-- Hidden file input for import -->
    <input type="file" id="importInput" accept=".json" style="display: none;" onchange="handleImport(event)">

    <script>
        // Translations
        const translations = {
            en: {
                app_title: "Furniture Orders Tracker",
                role_worker: "Worker",
                role_admin: "Workshop Manager",
                role_manager: "Manager",
                logout: "Logout",
                new_order: "New Order",
                statistics: "Statistics",
                export: "Export",
                import: "Import",
                search_orders: "🔍 Search orders...",
                all_priorities: "All Priorities",
                all_statuses: "All Statuses",
                all_types: "All Types",
                in_progress: "In Progress",
                completed: "Completed",
                with_problems: "With Problems",
                painted: "Painted",
                film: "Film",
                high: "High",
                medium: "Medium",
                low: "Low",
                order: "Order",
                client: "Client",
                name: "Name",
                quantity: "Qty",
                deadline: "Deadline",
                cost: "Cost",
                priority: "Priority",
                type: "Type",
                category: "Category",
                new: "New",
                cutting: "Cutting",
                edging: "Edging",
                cnc: "CNC",
                sanding: "Sanding",
                priming: "Priming",
                painting: "Painting",
                filming: "Filming",
                drilling: "Drilling",
                assembly: "Assembly",
                quality: "Quality",
                packing: "Packing",
                ready: "Ready",
                order_wizard: "Order Creation Wizard",
                basic_info: "Basic Information",
                materials: "Materials",
                tech_card: "Tech Card",
                files_dates: "Files & Dates",
                confirmation: "Confirmation",
                order_number: "Order Number",
                client_placeholder: "Company name or full name",
                product_name: "Product Name",
                quantity_units: "Quantity",
                coating_type: "Coating Type",
                select_type: "Select Type",
                product_category: "Product Category",
                select_category: "Select Category",
                mirror: "Mirror",
                cabinet: "Cabinet",
                nightstand: "Nightstand",
                led: "LED",
                order_cost: "Order Cost (₽)",
                order_description: "Order Description",
                description_placeholder: "Detailed product description, special requirements...",
                materials_selection: "Materials Selection",
                selected_materials: "Selected Materials:",
                no_materials: "No materials selected",
                upload_tech_card: "Upload Tech Card",
                tech_card_hint: "CSV, Excel files with material consumption data",
                parsed_materials: "Parsed Materials:",
                start_date: "Planned Start Date",
                deadline_date: "Desired Completion Date",
                file_upload: "File Upload",
                drag_files: "Drag files here or click to select",
                file_hint: "Drawings, photos, tech cards (up to 10 MB each)",
                order_confirmation: "Order Confirmation",
                back: "Back",
                next: "Next",
                create_order: "Create Order",
                mark_problem: "Mark Problem",
                problem_description: "Describe the problem:",
                problem_placeholder: "For example: no material, machine broken, waiting for drawings...",
                cancel: "Cancel",
                order_created: "✅ Order successfully created!",
                problem_marked: "⚠️ Problem recorded",
                step_completed: "✅ Step successfully completed!",
                problem_resolved: "🔄 Problem resolved, step returned to work",
                step_returned: "🔄 Step returned to work",
                data_exported: "📤 Data exported!",
                data_imported: "📥 Data successfully imported!",
                invalid_file: "❌ Invalid file format!",
                file_error: "❌ Error reading file!",
                goodbye: "💾 Data saved. Goodbye!",
                days_short: "d.",
                orders_count: "orders",
                tech_card_uploaded: "✅ Tech card uploaded and parsed!",
                tech_card_error: "❌ Error parsing tech card!",
                painted_orders: "Painted Orders",
                film_orders: "Film Orders", 
                total_revenue: "Total Revenue",
                material_costs: "Material Costs",
                completed_orders: "Completed Orders",
                admin_required: "❌ Administrator rights required to undo completed stages!",
                materials_breakdown: "Materials Breakdown",
                total_materials: "Total Materials Used",
                material_quantity: "Quantity",
                select_client: "Select Client",
                custom_order: "Custom Order"
            },
            ru: {
                app_title: "Трекер Заказов Мебели",
                role_worker: "Рабочий",
                role_admin: "Начальник цеха",
                role_manager: "Менеджер",
                logout: "Выход",
                new_order: "Новый заказ",
                statistics: "Статистика",
                export: "Экспорт",
                import: "Импорт",
                search_orders: "🔍 Поиск заказов...",
                all_priorities: "Все приоритеты",
                all_statuses: "Все статусы",
                all_types: "Все типы",
                in_progress: "В работе",
                completed: "Завершенные",
                with_problems: "С проблемами",
                painted: "Крашеные",
                film: "Пленочные",
                high: "Высокий",
                medium: "Средний",
                low: "Низкий",
                order: "Заказ",
                client: "Клиент",
                name: "Наименование",
                quantity: "Кол-во",
                deadline: "Сроки",
                cost: "Стоимость",
                priority: "Приоритет",
                type: "Тип",
                category: "Вид",
                new: "Новый",
                cutting: "Распил",
                edging: "Кромка",
                cnc: "ЧПУ",
                sanding: "Шлифовка",
                priming: "Грунтовка",
                painting: "Покраска",
                filming: "Пленка",
                drilling: "Присадка",
                assembly: "Сборка",
                quality: "ОТК",
                packing: "Упаковка",
                ready: "Готово",
                order_wizard: "Мастер создания заказа",
                basic_info: "Основная информация",
                materials: "Материалы",
                tech_card: "Техкарта",
                files_dates: "Файлы и сроки",
                confirmation: "Подтверждение",
                order_number: "Номер заказа",
                client_placeholder: "Название компании или ФИО",
                product_name: "Наименование изделия",
                quantity_units: "Количество единиц",
                coating_type: "Тип покрытия",
                select_type: "Выберите тип",
                product_category: "Вид изделия",
                select_category: "Выберите вид",
                mirror: "Зеркало",
                cabinet: "Пенал",
                nightstand: "Тумба",
                led: "LED",
                order_cost: "Стоимость заказа (₽)",
                order_description: "Описание заказа",
                description_placeholder: "Подробное описание изделия, особые требования...",
                materials_selection: "Выбор материалов",
                selected_materials: "Выбранные материалы:",
                no_materials: "Материалы не выбраны",
                upload_tech_card: "Загрузить техкарту",
                tech_card_hint: "CSV, Excel файлы с данными расхода материалов",
                parsed_materials: "Распознанные материалы:",
                start_date: "Планируемая дата начала",
                deadline_date: "Желаемая дата готовности",
                file_upload: "Загрузка файлов",
                drag_files: "Перетащите файлы сюда или нажмите для выбора",
                file_hint: "Чертежи, фотографии, техкарты (до 10 МБ каждый)",
                order_confirmation: "Подтверждение заказа",
                back: "Назад",
                next: "Далее",
                create_order: "Создать заказ",
                mark_problem: "Отметить проблему",
                problem_description: "Опишите причину проблемы:",
                problem_placeholder: "Например: нет материала, сломан станок, ожидаем чертежи...",
                cancel: "Отмена",
                order_created: "✅ Заказ успешно создан!",
                problem_marked: "⚠️ Проблема зафиксирована",
                step_completed: "✅ Этап успешно завершен!",
                problem_resolved: "🔄 Проблема решена, этап возвращен в работу",
                step_returned: "🔄 Этап возвращен в работу",
                data_exported: "📤 Данные экспортированы!",
                data_imported: "📥 Данные успешно импортированы!",
                invalid_file: "❌ Неверный формат файла!",
                file_error: "❌ Ошибка при чтении файла!",
                goodbye: "💾 Данные сохранены. До свидания!",
                days_short: "дн.",
                orders_count: "заказов",
                tech_card_uploaded: "✅ Техкарта загружена и обработана!",
                tech_card_error: "❌ Ошибка при обработке техкарты!",
                painted_orders: "Крашеные заказы",
                film_orders: "Пленочные заказы",
                total_revenue: "Общая выручка", 
                material_costs: "Затраты на материалы",
                completed_orders: "Завершенные заказы",
                admin_required: "❌ Необходимы права администратора для отмены завершенных этапов!",
                materials_breakdown: "Расход материалов",
                total_materials: "Всего использовано материалов",
                material_quantity: "Количество",
                select_client: "Выберите клиента",
                custom_order: "Под заказ"
            },
            ky: {
                app_title: "Эмерек Буйрутмаларынын Трекери",
                role_worker: "Жумушчу",
                role_admin: "Цех башчысы",
                role_manager: "Менеджер",
                logout: "Чыгуу",
                new_order: "Жаңы буйрутма",
                statistics: "Статистика",
                export: "Экспорт",
                import: "Импорт",
                search_orders: "🔍 Буйрутмаларды издөө...",
                all_priorities: "Бардык приоритеттер",
                all_statuses: "Бардык статустар",
                all_types: "Бардык түрлөр",
                in_progress: "Иштөө",
                completed: "Аяктаган",
                with_problems: "Көйгөйлөр менен",
                painted: "Боёлгон",
                film: "Пленка",
                high: "Жогорку",
                medium: "Орточо",
                low: "Төмөн",
                order: "Буйрутма",
                client: "Кардар",
                name: "Аталышы",
                quantity: "Саны",
                deadline: "Мөөнөт",
                cost: "Нарк",
                priority: "Приоритет",
                type: "Түр",
                category: "Категория",
                new: "Жаңы",
                cutting: "Кесүү",
                edging: "Четтөө",
                cnc: "ЧПУ",
                sanding: "Жылтыроо",
                priming: "Грунттоо",
                painting: "Боёо",
                filming: "Пленка",
                drilling: "Тешүү",
                assembly: "Чогултуу",
                quality: "Сапат",
                packing: "Таңгактоо",
                ready: "Даяр",
                order_wizard: "Буйрутма түзүү мастери",
                basic_info: "Негизги маалымат",
                materials: "Материалдар",
                tech_card: "Техкарта",
                files_dates: "Файлдар жана мөөнөттөр",
                confirmation: "Ырастоо",
                order_number: "Буйрутма номери",
                client_placeholder: "Компаниянын аталышы же толук аты",
                product_name: "Буюмдун аталышы",
                quantity_units: "Бирдиктердин саны",
                coating_type: "Каптама түрү",
                select_type: "Түрүн тандаңыз",
                product_category: "Буюм түрү",
                select_category: "Категорияны тандаңыз",
                mirror: "Күзгү",
                cabinet: "Шкаф",
                nightstand: "Тумба",
                led: "LED",
                order_cost: "Буйрутманын наркы (₽)",
                order_description: "Буйрутманын сыпаттамасы",
                description_placeholder: "Буюмдун толук сыпаттамасы, өзгөчө талаптар...",
                materials_selection: "Материалдарды тандоо",
                selected_materials: "Тандалган материалдар:",
                no_materials: "Материалдар тандалган жок",
                upload_tech_card: "Техкарта жүктөө",
                tech_card_hint: "CSV, Excel файлдар материалдардын чыгымы жөнүндө",
                parsed_materials: "Таанылган материалдар:",
                start_date: "Пландаштырылган башталуу күнү",
                deadline_date: "Каалаган бүтүрүү күнү",
                file_upload: "Файлдарды жүктөө",
                drag_files: "Файлдарды бул жерге таштаңыз же тандоо үчүн басыңыз",
                file_hint: "Сүрөттөр, сүрөттөр, техкарталар (ар бири 10 МБ чейин)",
                order_confirmation: "Буйрутманы ырастоо",
                back: "Артка",
                next: "Кийинки",
                create_order: "Буйрутма түзүү",
                mark_problem: "Көйгөй белгилөө",
                problem_description: "Көйгөйдүн себебин сыпаттаңыз:",
                problem_placeholder: "Мисалы: материал жок, станок бузулган, сүрөттөрдү күтүп жатабыз...",
                cancel: "Жокко чыгаруу",
                order_created: "✅ Буйрутма ийгиликтүү түзүлдү!",
                problem_marked: "⚠️ Көйгөй белгиленди",
                step_completed: "✅ Этап ийгиликтүү аяктады!",
                problem_resolved: "🔄 Көйгөй чечилди, этап ишке кайтарылды",
                step_returned: "🔄 Этап ишке кайтарылды",
                data_exported: "📤 Маалыматтар экспорттолду!",
                data_imported: "📥 Маалыматтар ийгиликтүү импорттолду!",
                invalid_file: "❌ Туура эмес файл форматы!",
                file_error: "❌ Файлды окууда ката!",
                goodbye: "💾 Маалыматтар сакталды. Кош болуңуз!",
                days_short: "к.",
                orders_count: "буйрутма",
                tech_card_uploaded: "✅ Техкарта жүктөлдү жана иштетилди!",
                tech_card_error: "❌ Техкартаны иштетүүдө ката!",
                painted_orders: "Боёлгон буйрутмалар",
                film_orders: "Пленкалуу буйрутмалар",
                total_revenue: "Жалпы киреше",
                material_costs: "Материалдарга чыгымдар", 
                completed_orders: "Аяктаган буйрутмалар",
                admin_required: "❌ Аяктаган этаптарды жокко чыгаруу үчүн администратор укугу керек!",
                materials_breakdown: "Материалдардын чыгымы",
                total_materials: "Жалпы колдонулган материалдар",
                material_quantity: "Саны",
                select_client: "Кардарды тандаңыз",
                custom_order: "Буйрутма боюнча"
            }
        };

        // Global variables
        const STAGES = ['new', 'cutting', 'edging', 'cnc', 'sanding', 'priming', 'painting', 'filming', 'drilling', 'assembly', 'quality', 'packing', 'ready'];
        
        let orders = [];
        let currentUser = { name: "Ivan Petrov", role: "admin" };
        let currentStep = 1;
        let selectedMaterials = [];
        let uploadedFiles = [];
        let parsedMaterials = [];
        let currentProblemOrderId = null;
        let currentProblemStageIndex = null;
        let currentLanguage = 'en';
        let currentMonth = new Date().getMonth();
        let currentYear = new Date().getFullYear();
        let monthlyMaterialsData = [];

        // Month names for animations
        const monthNames = ['january', 'february', 'march', 'april', 'may', 'june', 
                           'july', 'august', 'september', 'october', 'november', 'december'];

        // Materials catalog
        const MATERIALS_CATALOG = [
            { id: 1, name: "LDSP 16mm Oak Sonoma", category: "Plates", unit: "sheet", price: 1500 },
            { id: 2, name: "LDSP 16mm Wenge", category: "Plates", unit: "sheet", price: 1600 },
            { id: 3, name: "LDSP 18mm White", category: "Plates", unit: "sheet", price: 1400 },
            { id: 4, name: "PVC Edge 2mm Oak", category: "Edge", unit: "m", price: 25 },
            { id: 5, name: "PVC Edge 2mm Wenge", category: "Edge", unit: "m", price: 27 },
            { id: 6, name: "Blum Hardware", category: "Hardware", unit: "set", price: 3500 },
            { id: 7, name: "Slides 500mm", category: "Hardware", unit: "pair", price: 450 },
            { id: 8, name: "Overlay Hinges", category: "Hardware", unit: "pcs", price: 120 },
            { id: 9, name: "Glass 4mm", category: "Glass", unit: "m²", price: 800 },
            { id: 10, name: "Mirror 4mm", category: "Glass", unit: "m²", price: 1200 }
        ];

        // Language functions
        function setLanguage(lang) {
            currentLanguage = lang;
            localStorage.setItem('language', lang);
            
            // Update active language button
            document.querySelectorAll('.lang-btn').forEach(btn => {
                btn.classList.remove('active');
                if (btn.getAttribute('data-lang') === lang) {
                    btn.classList.add('active');
                }
            });
            
            updateTranslations();
        }

        function updateTranslations() {
            const elements = document.querySelectorAll('[data-translate]');
            elements.forEach(element => {
                const key = element.getAttribute('data-translate');
                if (translations[currentLanguage] && translations[currentLanguage][key]) {
                    element.textContent = translations[currentLanguage][key];
                }
            });

            // Update placeholders
            const placeholderElements = document.querySelectorAll('[data-translate-placeholder]');
            placeholderElements.forEach(element => {
                const key = element.getAttribute('data-translate-placeholder');
                if (translations[currentLanguage] && translations[currentLanguage][key]) {
                    element.placeholder = translations[currentLanguage][key];
                }
            });

            // Update select options and other dynamic content
            updateSelectOptions();
            updateCurrentMonth();
            renderOrders();
        }

        function updateSelectOptions() {
            // Priority filter
            const prioritySelect = document.getElementById('filterPriority');
            if (prioritySelect) {
                prioritySelect.innerHTML = `
                    <option value="">${translations[currentLanguage].all_priorities}</option>
                    <option value="high">${translations[currentLanguage].high}</option>
                    <option value="medium">${translations[currentLanguage].medium}</option>
                    <option value="low">${translations[currentLanguage].low}</option>
                `;
            }

            // Status filter
            const statusSelect = document.getElementById('filterStatus');
            if (statusSelect) {
                statusSelect.innerHTML = `
                    <option value="">${translations[currentLanguage].all_statuses}</option>
                    <option value="active">${translations[currentLanguage].in_progress}</option>
                    <option value="completed">${translations[currentLanguage].completed}</option>
                    <option value="problems">${translations[currentLanguage].with_problems}</option>
                `;
            }

            // Type filter
            const typeSelect = document.getElementById('filterType');
            if (typeSelect) {
                typeSelect.innerHTML = `
                    <option value="">${translations[currentLanguage].all_types}</option>
                    <option value="painted">${translations[currentLanguage].painted}</option>
                    <option value="film">${translations[currentLanguage].film}</option>
                `;
            }

            // Wizard selects
            const priorityWizard = document.getElementById('orderPriority');
            if (priorityWizard) {
                priorityWizard.innerHTML = `
                    <option value="low">🟢 ${translations[currentLanguage].low}</option>
                    <option value="medium" selected>🟡 ${translations[currentLanguage].medium}</option>
                    <option value="high">🔴 ${translations[currentLanguage].high}</option>
                `;
            }

            const typeWizard = document.getElementById('orderType');
            if (typeWizard) {
                typeWizard.innerHTML = `
                    <option value="">${translations[currentLanguage].select_type}</option>
                    <option value="painted">🎨 ${translations[currentLanguage].painted}</option>
                    <option value="film">📄 ${translations[currentLanguage].film}</option>
                `;
            }

            const categoryWizard = document.getElementById('orderCategory');
            if (categoryWizard) {
                categoryWizard.innerHTML = `
                    <option value="">${translations[currentLanguage].select_category}</option>
                    <option value="mirror">🪞 ${translations[currentLanguage].mirror}</option>
                    <option value="cabinet">📦 ${translations[currentLanguage].cabinet}</option>
                    <option value="nightstand">🪑 ${translations[currentLanguage].nightstand}</option>
                    <option value="led">💡 ${translations[currentLanguage].led}</option>
                `;
            }

            // Client selector
            const clientSelect = document.getElementById('clientName');
            if (clientSelect) {
                clientSelect.innerHTML = `
                    <option value="">${translations[currentLanguage].select_client}</option>
                    <option value="WASSER">WASSER</option>
                    <option value="custom">${translations[currentLanguage].custom_order}</option>
                `;
            }
        }

        // Client selection handler
        function handleClientSelection() {
            const clientSelect = document.getElementById('clientName');
            const customInput = document.getElementById('customClientName');
            
            if (clientSelect && customInput) {
                if (clientSelect.value === 'custom') {
                    customInput.style.display = 'block';
                    customInput.required = true;
                } else {
                    customInput.style.display = 'none';
                    customInput.required = false;
                    customInput.value = '';
                }
            }
        }

        // Setup client selector on wizard open
        function setupClientSelector() {
            const clientSelect = document.getElementById('clientName');
            if (clientSelect) {
                clientSelect.addEventListener('change', handleClientSelection);
            }
        }

        function t(key) {
            return translations[currentLanguage] && translations[currentLanguage][key] 
                ? translations[currentLanguage][key] 
                : key;
        }

        // Pagination functions
        function updateCurrentMonth() {
            const monthNamesLang = {
                en: ['January', 'February', 'March', 'April', 'May', 'June', 
                     'July', 'August', 'September', 'October', 'November', 'December'],
                ru: ['Январь', 'Февраль', 'Март', 'Апрель', 'Май', 'Июнь',
                     'Июль', 'Август', 'Сентябрь', 'Октябрь', 'Ноябрь', 'Декабрь'],
                ky: ['Январь', 'Февраль', 'Март', 'Апрель', 'Май', 'Июнь',
                     'Июль', 'Август', 'Сентябрь', 'Октябрь', 'Ноябрь', 'Декабрь']
            };
            
            const currentMonthElement = document.getElementById('currentMonth');
            if (currentMonthElement) {
                currentMonthElement.textContent = `${monthNamesLang[currentLanguage][currentMonth]} ${currentYear}`;
            }
            
            // Update month animation
            updateMonthAnimation();
            
            updateOrdersCount();
        }

        function updateMonthAnimation() {
            const animationElement = document.getElementById('monthAnimation');
            if (animationElement) {
                // Remove all existing month classes
                monthNames.forEach(month => {
                    animationElement.classList.remove(month);
                });
                
                // Add current month class
                animationElement.classList.add(monthNames[currentMonth]);
            }
        }

        function updateOrdersCount() {
            const filteredOrders = getFilteredOrdersByMonth();
            const ordersCountElement = document.getElementById('ordersCount');
            if (ordersCountElement) {
                ordersCountElement.textContent = `${filteredOrders.length} ${t('orders_count')}`;
            }
            
            // Update statistics
            updateMonthlyStatistics(filteredOrders);
        }

        function updateMonthlyStatistics(monthOrders) {
            let paintedCount = 0;
            let filmCount = 0;
            let totalRevenue = 0;
            let materialCost = 0;
            let completedCount = 0;

            // Reset materials data for the month
            monthlyMaterialsData = [];
            const materialsMap = new Map();

            monthOrders.forEach(order => {
                // Count by type
                if (order.type === 'painted') paintedCount++;
                if (order.type === 'film') filmCount++;

                // Calculate revenue
                if (order.cost) totalRevenue += order.cost;

                // Calculate material costs and collect materials data
                if (order.materials) {
                    order.materials.forEach(material => {
                        const cost = (material.price || 0) * (material.quantity || 0);
                        materialCost += cost;

                        // Collect materials for detailed breakdown
                        const key = material.name;
                        if (materialsMap.has(key)) {
                            const existing = materialsMap.get(key);
                            existing.quantity += material.quantity || 0;
                            existing.totalCost += cost;
                        } else {
                            materialsMap.set(key, {
                                name: material.name,
                                unit: material.unit || 'pcs',
                                quantity: material.quantity || 0,
                                pricePerUnit: material.price || 0,
                                totalCost: cost
                            });
                        }
                    });
                }

                // Count completed orders
                if (order.stages.every(stage => stage === 'completed')) {
                    completedCount++;
                }
            });

            // Convert materials map to array
            monthlyMaterialsData = Array.from(materialsMap.values()).sort((a, b) => b.totalCost - a.totalCost);

            // Update UI
            const paintedElement = document.getElementById('paintedCount');
            const filmElement = document.getElementById('filmCount');
            const revenueElement = document.getElementById('totalRevenue');
            const materialElement = document.getElementById('materialCost');
            const completedElement = document.getElementById('completedCount');

            if (paintedElement) paintedElement.textContent = paintedCount;
            if (filmElement) filmElement.textContent = filmCount;
            if (revenueElement) revenueElement.textContent = totalRevenue.toLocaleString() + '₽';
            if (materialElement) materialElement.textContent = materialCost.toLocaleString() + '₽';
            if (completedElement) completedElement.textContent = completedCount;
        }

        // Materials details modal functions
        function showMaterialsDetails() {
            const modal = document.getElementById('materialsModal');
            const breakdown = document.getElementById('materialsBreakdown');
            
            if (monthlyMaterialsData.length === 0) {
                breakdown.innerHTML = `
                    <div style="text-align: center; padding: 2rem; color: var(--text-secondary);">
                        <div style="font-size: 3rem; margin-bottom: 1rem;">📦</div>
                        <p>No materials data for this month</p>
                    </div>
                `;
            } else {
                const totalQuantity = monthlyMaterialsData.reduce((sum, material) => sum + material.quantity, 0);
                const totalCost = monthlyMaterialsData.reduce((sum, material) => sum + material.totalCost, 0);
                
                breakdown.innerHTML = `
                    <div style="background: var(--background-color); padding: 1.5rem; border-radius: 0.375rem; margin-bottom: 1.5rem; border: 1px solid var(--border-color);">
                        <h4>${t('total_materials')}</h4>
                        <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(150px, 1fr)); gap: 1rem; margin-top: 1rem;">
                            <div style="text-align: center;">
                                <div style="font-size: 1.5rem; font-weight: 700; color: var(--primary-color);">${monthlyMaterialsData.length}</div>
                                <div style="font-size: 0.875rem; color: var(--text-secondary);">Types</div>
                            </div>
                            <div style="text-align: center;">
                                <div style="font-size: 1.5rem; font-weight: 700; color: var(--primary-color);">${totalQuantity.toLocaleString()}</div>
                                <div style="font-size: 0.875rem; color: var(--text-secondary);">Units</div>
                            </div>
                            <div style="text-align: center;">
                                <div style="font-size: 1.5rem; font-weight: 700; color: var(--primary-color);">${totalCost.toLocaleString()}₽</div>
                                <div style="font-size: 0.875rem; color: var(--text-secondary);">Total Cost</div>
                            </div>
                        </div>
                    </div>
                    
                    <div style="background: var(--surface-color); border-radius: 0.375rem; overflow: hidden; border: 1px solid var(--border-color);">
                        <div style="background: var(--background-color); padding: 1rem; border-bottom: 1px solid var(--border-color); font-weight: 600;">
                            Material Details
                        </div>
                        <div style="max-height: 400px; overflow-y: auto;">
                            ${monthlyMaterialsData.map(material => `
                                <div style="display: flex; justify-content: space-between; align-items: center; padding: 1rem; border-bottom: 1px solid var(--border-color);">
                                    <div style="flex: 1;">
                                        <div style="font-weight: 600; margin-bottom: 0.25rem;">${material.name}</div>
                                        <div style="font-size: 0.875rem; color: var(--text-secondary);">
                                            ${material.quantity} ${material.unit} × ${material.pricePerUnit.toLocaleString()}₽
                                        </div>
                                    </div>
                                    <div style="text-align: right;">
                                        <div style="font-weight: 700; color: var(--primary-color);">${material.totalCost.toLocaleString()}₽</div>
                                    </div>
                                </div>
                            `).join('')}
                        </div>
                    </div>
                `;
            }
            
            modal.style.display = 'block';
        }

        function closeMaterialsModal() {
            const modal = document.getElementById('materialsModal');
            modal.style.display = 'none';
        }

        function previousMonth() {
            if (currentMonth === 0) {
                currentMonth = 11;
                currentYear--;
            } else {
                currentMonth--;
            }
            updateCurrentMonth();
            renderOrders();
        }

        function nextMonth() {
            if (currentMonth === 11) {
                currentMonth = 0;
                currentYear++;
            } else {
                currentMonth++;
            }
            updateCurrentMonth();
            renderOrders();
        }

        function getFilteredOrdersByMonth() {
            return orders.filter(order => {
                const orderDate = new Date(order.date);
                return orderDate.getMonth() === currentMonth && orderDate.getFullYear() === currentYear;
            });
        }

        // Initialize app
        document.addEventListener('DOMContentLoaded', function() {
            loadLanguage();
            loadDataFromStorage();
            setupUserInterface();
            renderOrders();
            setupFileUpload();
            setupTechCardUpload();
            loadTheme();
            startAutoSave();
            updateTranslations();
            updateMonthAnimation(); // Initialize month animation
        });

        function loadLanguage() {
            const savedLanguage = localStorage.getItem('language') || 'en';
            setLanguage(savedLanguage);
        }

        // Theme management
        function toggleTheme() {
            const currentTheme = document.documentElement.getAttribute('data-theme') || 'light';
            const newTheme = currentTheme === 'light' ? 'dark' : 'light';
            
            document.documentElement.setAttribute('data-theme', newTheme);
            document.getElementById('themeIcon').textContent = newTheme === 'light' ? '🌙' : '☀️';
            localStorage.setItem('theme', newTheme);
        }

        function loadTheme() {
            const savedTheme = localStorage.getItem('theme') || 'light';
            document.documentElement.setAttribute('data-theme', savedTheme);
            document.getElementById('themeIcon').textContent = savedTheme === 'light' ? '🌙' : '☀️';
        }

        // Data management
        function loadDataFromStorage() {
            const savedOrders = localStorage.getItem('furnitureOrdersV5');
            if (savedOrders) {
                orders = JSON.parse(savedOrders);
            } else {
                // Demo data
                orders = [
                    {
                        id: "2024-001",
                        date: new Date().toISOString().split('T')[0],
                        clientName: "Construction Ltd",
                        name: "Classic Kitchen Set",
                        description: "Classic style kitchen set with MDF facades",
                        quantity: 1,
                        type: "painted",
                        category: "cabinet",
                        priority: "high",
                        cost: 85000,
                        startDate: new Date().toISOString().split('T')[0],
                        deadline: new Date(Date.now() + 14 * 24 * 60 * 60 * 1000).toISOString().split('T')[0],
                        materials: [
                            { id: 1, name: "LDSP 16mm Oak Sonoma", quantity: 5, unit: "sheet", price: 1500 },
                            { id: 4, name: "PVC Edge 2mm Oak", quantity: 50, unit: "m", price: 25 },
                            { id: 6, name: "Blum Hardware", quantity: 1, unit: "set", price: 3500 }
                        ],
                        stages: ["completed", "completed", "problem", "pending", "pending", "pending", "pending", "pending", "pending", "pending", "pending", "pending", "pending"],
                        stageTimestamps: {
                            0: new Date(Date.now() - 172800000).toISOString(), // 2 days ago
                            1: new Date(Date.now() - 86400000).toISOString(),  // 1 day ago
                            2: new Date(Date.now() - 43200000).toISOString()   // 12 hours ago
                        },
                        history: [
                            { time: new Date(), user: "System", action: "Order created", stage: "new" },
                            { time: new Date(Date.now() - 86400000), user: "Peter Sidorov", action: "Stage completed: Cutting", stage: "cutting" },
                            { time: new Date(Date.now() - 43200000), user: "Maria Ivanova", action: "Problem: no material", stage: "edging" }
                        ],
                        comments: "Urgent order for VIP client",
                        files: [],
                        techCard: null
                    },
                    {
                        id: "2024-002",
                        date: new Date().toISOString().split('T')[0],
                        clientName: "Modern Homes LLC",
                        name: "Bedroom Set",
                        description: "Modern bedroom furniture with film coating",
                        quantity: 2,
                        type: "film",
                        category: "nightstand",
                        priority: "medium",
                        cost: 45000,
                        startDate: new Date().toISOString().split('T')[0],
                        deadline: new Date(Date.now() + 21 * 24 * 60 * 60 * 1000).toISOString().split('T')[0],
                        materials: [
                            { id: 2, name: "LDSP 16mm Wenge", quantity: 3, unit: "sheet", price: 1600 },
                            { id: 5, name: "PVC Edge 2mm Wenge", quantity: 30, unit: "m", price: 27 }
                        ],
                        stages: ["completed", "completed", "completed", "completed", "pending", "pending", "pending", "completed", "pending", "pending", "pending", "pending", "pending"],
                        stageTimestamps: {
                            0: new Date(Date.now() - 345600000).toISOString(), // 4 days ago
                            1: new Date(Date.now() - 259200000).toISOString(), // 3 days ago
                            2: new Date(Date.now() - 172800000).toISOString(), // 2 days ago
                            3: new Date(Date.now() - 86400000).toISOString(),  // 1 day ago
                            7: new Date(Date.now() - 21600000).toISOString()   // 6 hours ago
                        },
                        history: [
                            { time: new Date(), user: "System", action: "Order created", stage: "new" }
                        ],
                        comments: "",
                        files: [],
                        techCard: null
                    }
                ];
                saveDataToStorage();
            }
        }

        function saveDataToStorage() {
            localStorage.setItem('furnitureOrdersV5', JSON.stringify(orders));
        }

        function startAutoSave() {
            setInterval(saveDataToStorage, 30000);
        }

        // User interface setup
        function setupUserInterface() {
            const roleElement = document.getElementById('userRole');
            const newOrderBtn = document.getElementById('newOrderBtn');
            const statsBtn = document.getElementById('statsBtn');

            switch(currentUser.role) {
                case 'worker':
                    roleElement.setAttribute('data-translate', 'role_worker');
                    newOrderBtn.style.display = 'none';
                    statsBtn.style.display = 'none';
                    break;
                case 'admin':
                    roleElement.setAttribute('data-translate', 'role_admin');
                    break;
                case 'manager':
                    roleElement.setAttribute('data-translate', 'role_manager');
                    newOrderBtn.style.display = 'none';
                    break;
            }
            
            document.getElementById('userName').textContent = currentUser.name;
        }

        // Tech Card Upload and Parsing
        function setupTechCardUpload() {
            const uploadArea = document.getElementById('techCardUpload');
            const fileInput = document.getElementById('techCardInput');
            
            if (!uploadArea || !fileInput) return;
            
            uploadArea.addEventListener('dragover', (e) => {
                e.preventDefault();
                uploadArea.classList.add('dragover');
            });
            
            uploadArea.addEventListener('dragleave', () => {
                uploadArea.classList.remove('dragover');
            });
            
            uploadArea.addEventListener('drop', (e) => {
                e.preventDefault();
                uploadArea.classList.remove('dragover');
                handleTechCardUpload({ target: { files: e.dataTransfer.files } });
            });
        }

        function handleTechCardUpload(event) {
            const file = event.target.files[0];
            if (!file) return;

            const reader = new FileReader();
            reader.onload = function(e) {
                try {
                    if (file.name.endsWith('.csv')) {
                        parseCSVTechCard(e.target.result);
                    } else if (file.name.endsWith('.xlsx') || file.name.endsWith('.xls')) {
                        // For Excel files, we'll simulate parsing since we can't use actual Excel libraries in this environment
                        parseExcelTechCard(file);
                    }
                } catch (error) {
                    showNotification(t('tech_card_error'), 'error');
                }
            };
            
            if (file.name.endsWith('.csv')) {
                reader.readAsText(file);
            } else {
                reader.readAsArrayBuffer(file);
            }
        }

        function parseCSVTechCard(csvContent) {
            const lines = csvContent.split('\n');
            const materials = [];
            
            // Skip header row, assume format: Material Name, Quantity, Unit
            for (let i = 1; i < lines.length; i++) {
                const line = lines[i].trim();
                if (!line) continue;
                
                const columns = line.split(',').map(col => col.trim().replace(/"/g, ''));
                if (columns.length >= 3) {
                    const materialName = columns[0];
                    const quantity = parseFloat(columns[1]);
                    const unit = columns[2];
                    
                    if (materialName && !isNaN(quantity) && unit) {
                        // Try to find matching material in catalog
                        const catalogMaterial = MATERIALS_CATALOG.find(m => 
                            m.name.toLowerCase().includes(materialName.toLowerCase()) ||
                            materialName.toLowerCase().includes(m.name.toLowerCase())
                        );
                        
                        materials.push({
                            id: catalogMaterial ? catalogMaterial.id : Math.random() * 1000,
                            name: materialName,
                            quantity: quantity,
                            unit: unit,
                            price: catalogMaterial ? catalogMaterial.price : 0,
                            fromTechCard: true
                        });
                    }
                }
            }
            
            displayParsedMaterials(materials);
        }

        function parseExcelTechCard(file) {
            // Simulated Excel parsing - in a real application, you'd use a library like SheetJS
            const simulatedMaterials = [
                { id: 1, name: "LDSP 16mm Oak Sonoma", quantity: 3, unit: "sheet", price: 1500, fromTechCard: true },
                { id: 4, name: "PVC Edge 2mm Oak", quantity: 25, unit: "m", price: 25, fromTechCard: true },
                { id: 6, name: "Blum Hardware", quantity: 1, unit: "set", price: 3500, fromTechCard: true }
            ];
            
            displayParsedMaterials(simulatedMaterials);
        }

        function displayParsedMaterials(materials) {
            parsedMaterials = materials;
            const resultsDiv = document.getElementById('techCardResults');
            const materialsDiv = document.getElementById('parsedMaterials');
            
            if (materials.length > 0) {
                resultsDiv.style.display = 'block';
                materialsDiv.innerHTML = materials.map(material => `
                    <div class="material-item">
                        <div>
                            <strong>${material.name}</strong><br>
                            <span style="color: var(--text-secondary); font-size: 0.875rem;">
                                ${material.quantity} ${material.unit} × ${material.price}₽ = ${(material.quantity * material.price).toLocaleString()}₽
                            </span>
                        </div>
                        <button class="btn btn-success" onclick="addParsedMaterial(${material.id})" style="padding: 0.5rem 1rem; font-size: 0.75rem;">
                            Add to Order
                        </button>
                    </div>
                `).join('');
                
                showNotification(t('tech_card_uploaded'));
            } else {
                showNotification(t('tech_card_error'), 'error');
            }
        }

        function addParsedMaterial(materialId) {
            const material = parsedMaterials.find(m => m.id === materialId);
            if (material) {
                // Check if already exists in selected materials
                const existingIndex = selectedMaterials.findIndex(m => m.id === materialId);
                if (existingIndex >= 0) {
                    selectedMaterials[existingIndex].quantity += material.quantity;
                } else {
                    selectedMaterials.push({...material});
                }
                updateMaterialsDisplay();
                showNotification(`✅ ${material.name} added to order`);
            }
        }

        // Order wizard
        function showOrderWizard() {
            currentStep = 1;
            selectedMaterials = [];
            uploadedFiles = [];
            parsedMaterials = [];
            
            generateOrderNumber();
            setDefaultDates();
            renderMaterialsCatalog();
            updateWizardDisplay();
            updateSelectOptions();
            setupClientSelector();
            
            const modal = document.getElementById('orderWizard');
            modal.style.display = 'block';
        }

        function closeOrderWizard() {
            const modal = document.getElementById('orderWizard');
            modal.style.display = 'none';
            
            // Reset tech card results
            const resultsDiv = document.getElementById('techCardResults');
            if (resultsDiv) resultsDiv.style.display = 'none';
        }

        function generateOrderNumber() {
            const year = new Date().getFullYear();
            const nextNumber = String(orders.length + 1).padStart(3, '0');
            document.getElementById('orderNumber').value = `${year}-${nextNumber}`;
        }

        function setDefaultDates() {
            const today = new Date().toISOString().split('T')[0];
            const weekLater = new Date(Date.now() + 14 * 24 * 60 * 60 * 1000).toISOString().split('T')[0];
            
            document.getElementById('orderStartDate').value = today;
            document.getElementById('orderDeadline').value = weekLater;
        }

        function renderMaterialsCatalog() {
            const catalog = document.getElementById('materialsCatalog');
            if (!catalog) return;
            
            catalog.innerHTML = MATERIALS_CATALOG.map(material => `
                <div class="material-card" onclick="toggleMaterial(${material.id})" style="background: var(--surface-color); border: 1px solid var(--border-color); border-radius: 0.375rem; padding: 1rem; cursor: pointer; transition: var(--transition);">
                    <div style="font-weight: 600; margin-bottom: 0.5rem;">${material.name}</div>
                    <div style="font-size: 0.875rem; color: var(--text-secondary);">${material.category} • ${material.price}₽/${material.unit}</div>
                </div>
            `).join('');
        }

        function toggleMaterial(materialId) {
            const material = MATERIALS_CATALOG.find(m => m.id === materialId);
            const existingIndex = selectedMaterials.findIndex(m => m.id === materialId);
            
            if (existingIndex >= 0) {
                selectedMaterials.splice(existingIndex, 1);
            } else {
                const quantity = prompt(`Specify quantity for "${material.name}" (${material.unit}):`);
                if (quantity && !isNaN(quantity) && quantity > 0) {
                    selectedMaterials.push({
                        ...material,
                        quantity: parseFloat(quantity)
                    });
                }
            }
            
            updateMaterialsDisplay();
        }

        function updateMaterialsDisplay() {
            const container = document.getElementById('selectedMaterials');
            if (!container) return;
            
            if (selectedMaterials.length === 0) {
                container.innerHTML = `<p style="color: var(--text-secondary); text-align: center;">${t('no_materials')}</p>`;
            } else {
                container.innerHTML = selectedMaterials.map(material => `
                    <div class="material-item" style="display: flex; justify-content: space-between; align-items: center; padding: 1rem; background: var(--surface-color); border-radius: 0.375rem; margin-bottom: 0.75rem; border: 1px solid var(--border-color);">
                        <span><strong>${material.name}</strong> - ${material.quantity} ${material.unit}</span>
                        <button class="btn btn-danger" onclick="removeMaterial(${material.id})" style="padding: 0.5rem 1rem; font-size: 0.75rem;">${t('cancel')}</button>
                    </div>
                `).join('');
            }
            
            // Update visual selection in catalog
            document.querySelectorAll('.material-card').forEach((card, index) => {
                const material = MATERIALS_CATALOG[index];
                const isSelected = selectedMaterials.some(m => m.id === material.id);
                if (isSelected) {
                    card.style.borderColor = 'var(--primary-color)';
                    card.style.backgroundColor = 'rgba(37, 99, 235, 0.05)';
                } else {
                    card.style.borderColor = 'var(--border-color)';
                    card.style.backgroundColor = 'var(--surface-color)';
                }
            });
        }

        function removeMaterial(materialId) {
            selectedMaterials = selectedMaterials.filter(m => m.id !== materialId);
            updateMaterialsDisplay();
        }

        // File upload setup
        function setupFileUpload() {
            const uploadArea = document.getElementById('fileUploadArea');
            const fileInput = document.getElementById('fileInput');
            
            if (!uploadArea || !fileInput) return;
            
            uploadArea.addEventListener('dragover', (e) => {
                e.preventDefault();
                uploadArea.classList.add('dragover');
            });
            
            uploadArea.addEventListener('dragleave', () => {
                uploadArea.classList.remove('dragover');
            });
            
            uploadArea.addEventListener('drop', (e) => {
                e.preventDefault();
                uploadArea.classList.remove('dragover');
                handleFiles(e.dataTransfer.files);
            });
            
            fileInput.addEventListener('change', (e) => {
                handleFiles(e.target.files);
            });
        }

        function handleFiles(files) {
            Array.from(files).forEach(file => {
                if (file.size <= 10 * 1024 * 1024) { // 10MB limit
                    uploadedFiles.push({
                        name: file.name,
                        size: formatFileSize(file.size),
                        type: file.type
                    });
                } else {
                    showNotification(`File ${file.name} is too large (maximum 10 MB)`, 'error');
                }
            });
            updateFilesList();
        }

        function updateFilesList() {
            const filesList = document.getElementById('filesList');
            if (!filesList) return;
            
            if (uploadedFiles.length === 0) {
                filesList.innerHTML = '';
            } else {
                filesList.innerHTML = `
                    <h4 style="margin-top: 1.5rem; margin-bottom: 1rem;">Uploaded files:</h4>
                    ${uploadedFiles.map((file, index) => `
                        <div class="material-item" style="display: flex; justify-content: space-between; align-items: center; padding: 1rem; background: var(--surface-color); border-radius: 0.375rem; margin-bottom: 0.75rem; border: 1px solid var(--border-color);">
                            <span>📎 ${file.name} (${file.size})</span>
                            <button class="btn btn-danger" onclick="removeFile(${index})" style="padding: 0.5rem 1rem; font-size: 0.75rem;">${t('cancel')}</button>
                        </div>
                    `).join('')}
                `;
            }
        }

        function removeFile(index) {
            uploadedFiles.splice(index, 1);
            updateFilesList();
        }

        // Wizard navigation
        function nextStep() {
            if (validateCurrentStep()) {
                if (currentStep < 5) {
                    currentStep++;
                    updateWizardDisplay();
                }
            }
        }

        function previousStep() {
            if (currentStep > 1) {
                currentStep--;
                updateWizardDisplay();
            }
        }

        function updateWizardDisplay() {
            // Update step indicators
            for (let i = 1; i <= 5; i++) {
                const circle = document.getElementById(`step${i}Circle`);
                const content = document.getElementById(`step${i}`);
                
                if (!circle || !content) continue;
                
                circle.classList.remove('active', 'completed');
                content.classList.remove('active');
                
                if (i < currentStep) {
                    circle.classList.add('completed');
                    circle.innerHTML = '✓';
                } else if (i === currentStep) {
                    circle.classList.add('active');
                    circle.innerHTML = i;
                    content.classList.add('active');
                } else {
                    circle.innerHTML = i;
                }
            }
            
            // Update buttons
            const prevBtn = document.getElementById('prevBtn');
            const nextBtn = document.getElementById('nextBtn');
            const createBtn = document.getElementById('createBtn');
            
            if (prevBtn) prevBtn.style.display = currentStep > 1 ? 'block' : 'none';
            if (nextBtn) nextBtn.style.display = currentStep < 5 ? 'block' : 'none';
            if (createBtn) createBtn.style.display = currentStep === 5 ? 'block' : 'none';
            
            // Generate summary for step 5
            if (currentStep === 5) {
                generateOrderSummary();
            }
        }

        function validateCurrentStep() {
            switch (currentStep) {
                case 1:
                    const required1 = ['orderNumber', 'clientName', 'orderName', 'orderQuantity', 'orderType', 'orderCategory'];
                    for (let field of required1) {
                        const element = document.getElementById(field);
                        if (!element || !element.value.trim()) {
                            showNotification('Please fill all required fields', 'error');
                            return false;
                        }
                    }
                    break;
                case 2:
                    if (selectedMaterials.length === 0) {
                        showNotification('Please select at least one material', 'error');
                        return false;
                    }
                    break;
                case 3:
                case 4:
                    // Tech card and files are optional
                    break;
            }
            return true;
        }

        function generateOrderSummary() {
            const orderData = collectOrderData();
            const totalCost = selectedMaterials.reduce((sum, material) => sum + (material.price * material.quantity), 0);
            
            const summaryContainer = document.getElementById('orderSummary');
            if (!summaryContainer) return;
            
            summaryContainer.innerHTML = `
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 2rem;">
                    <div style="background: var(--background-color); padding: 1.5rem; border-radius: 0.375rem; border: 1px solid var(--border-color);">
                        <h4>📋 ${t('basic_info')}</h4>
                        <p><strong>${t('order_number')}:</strong> ${orderData.id}</p>
                        <p><strong>${t('client')}:</strong> ${orderData.clientName}</p>
                        <p><strong>${t('product_name')}:</strong> ${orderData.name}</p>
                        <p><strong>${t('quantity')}:</strong> ${orderData.quantity} pcs</p>
                        <p><strong>${t('type')}:</strong> ${t(orderData.type)}</p>
                        <p><strong>${t('category')}:</strong> ${t(orderData.category)}</p>
                        <p><strong>${t('priority')}:</strong> ${t(orderData.priority)}</p>
                        <p><strong>${t('order_cost')}:</strong> ${orderData.cost ? orderData.cost.toLocaleString() + '₽' : 'Not specified'}</p>
                    </div>
                    
                    <div style="background: var(--background-color); padding: 1.5rem; border-radius: 0.375rem; border: 1px solid var(--border-color);">
                        <h4>📦 ${t('materials')}</h4>
                        ${selectedMaterials.map(material => `
                            <p>${material.name} - ${material.quantity} ${material.unit} (${(material.price * material.quantity).toLocaleString()}₽)</p>
                        `).join('')}
                        <hr style="margin: 1rem 0; border: 1px solid var(--border-color);">
                        <p><strong>Materials cost: ${totalCost.toLocaleString()}₽</strong></p>
                    </div>
                    
                    <div style="background: var(--background-color); padding: 1.5rem; border-radius: 0.375rem; border: 1px solid var(--border-color);">
                        <h4>📅 ${t('files_dates')}</h4>
                        <p><strong>${t('start_date')}:</strong> ${formatDate(orderData.startDate)}</p>
                        <p><strong>${t('deadline_date')}:</strong> ${formatDate(orderData.deadline)}</p>
                        <p><strong>Files uploaded:</strong> ${uploadedFiles.length} pcs</p>
                        <p><strong>Tech card:</strong> ${parsedMaterials.length > 0 ? 'Uploaded' : 'Not uploaded'}</p>
                    </div>
                    
                    <div style="background: var(--background-color); padding: 1.5rem; border-radius: 0.375rem; border: 1px solid var(--border-color);">
                        <h4>💭 ${t('order_description')}</h4>
                        <p>${orderData.description || 'Not specified'}</p>
                    </div>
                </div>
            `;
        }

        function collectOrderData() {
            const clientSelect = document.getElementById('clientName');
            const customClientInput = document.getElementById('customClientName');
            
            let clientName = '';
            if (clientSelect && clientSelect.value) {
                if (clientSelect.value === 'custom' && customClientInput) {
                    clientName = customClientInput.value;
                } else {
                    clientName = clientSelect.value;
                }
            }
            
            return {
                id: document.getElementById('orderNumber')?.value || '',
                clientName: clientName,
                name: document.getElementById('orderName')?.value || '',
                description: document.getElementById('orderDescription')?.value || '',
                quantity: parseInt(document.getElementById('orderQuantity')?.value) || 1,
                type: document.getElementById('orderType')?.value || '',
                category: document.getElementById('orderCategory')?.value || '',
                priority: document.getElementById('orderPriority')?.value || 'medium',
                cost: parseFloat(document.getElementById('orderCost')?.value) || 0,
                startDate: document.getElementById('orderStartDate')?.value || '',
                deadline: document.getElementById('orderDeadline')?.value || ''
            };
        }

        function createOrder() {
            const orderData = collectOrderData();
            
            // Check if order number is unique
            if (orders.find(o => o.id === orderData.id)) {
                showNotification('Order with this number already exists!', 'error');
                return;
            }
            
            const newOrder = {
                ...orderData,
                date: new Date().toISOString().split('T')[0],
                materials: selectedMaterials,
                stages: ['completed', ...new Array(12).fill('pending')],
                stageTimestamps: {
                    0: new Date().toISOString()
                },
                history: [{
                    time: new Date(),
                    user: currentUser.name,
                    action: "Order created",
                    stage: "new"
                }],
                comments: "",
                files: uploadedFiles,
                techCard: parsedMaterials.length > 0 ? parsedMaterials : null
            };
            
            orders.unshift(newOrder);
            saveDataToStorage();
            renderOrders();
            closeOrderWizard();
            showNotification(t('order_created'));
        }

        // Type restrictions for stages
        function updateTypeRestrictions() {
            // This function will handle stage restrictions based on coating type
            const orderType = document.getElementById('orderType')?.value;
            console.log('Type changed to:', orderType);
        }

        // Orders rendering
        function renderOrders() {
            const tbody = document.getElementById('ordersTableBody');
            if (!tbody) return;
            
            tbody.innerHTML = '';
            
            const filteredOrders = getFilteredOrders();
            
            filteredOrders.forEach(order => {
                const row = document.createElement('tr');
                
                // Check for problems and apply row styling
                const hasProblem = order.stages.includes('problem');
                if (hasProblem) {
                    row.classList.add('problem-order');
                } else if (order.type === 'painted') {
                    row.classList.add('painted-order');
                } else if (order.type === 'film') {
                    row.classList.add('film-order');
                }
                
                row.innerHTML = `
                    <td>
                        <div class="order-number" onclick="openOrderDetails('${order.id}')">${order.id}</div>
                        <div class="order-meta">${formatDate(order.date)}</div>
                    </td>
                    <td>
                        <div style="font-weight: 600;">${order.clientName}</div>
                    </td>
                    <td>
                        <div style="font-weight: 500;">${order.name}</div>
                        <div class="order-meta">${order.description ? order.description.substring(0, 40) + '...' : ''}</div>
                    </td>
                    <td>${order.quantity} pcs</td>
                    <td>
                        <div>to ${formatDate(order.deadline)}</div>
                        <div class="order-meta">${getDaysRemaining(order.deadline)} ${t('days_short')}</div>
                    </td>
                    <td>${order.cost ? order.cost.toLocaleString() + '₽' : '—'}</td>
                    <td>
                        <span class="priority-badge priority-${order.priority}">
                            ${t(order.priority)}
                        </span>
                    </td>
                    <td>
                        <span class="type-badge type-${order.type}">
                            ${t(order.type)}
                        </span>
                    </td>
                    <td>
                        ${t(order.category)}
                    </td>
                `;
                
                // Add stage indicators
                order.stages.forEach((status, index) => {
                    const cell = document.createElement('td');
                    cell.className = 'stage-cell';
                    
                    const container = document.createElement('div');
                    container.style.display = 'flex';
                    container.style.flexDirection = 'column';
                    container.style.alignItems = 'center';
                    
                    const indicator = document.createElement('div');
                    indicator.className = `status-indicator status-${status}`;
                    
                    // Check if stage should be disabled based on type
                    const isDisabled = shouldStageBeDisabled(order.type, index);
                    if (isDisabled) {
                        indicator.classList.add('disabled');
                        indicator.innerHTML = '—';
                    } else {
                        if (status === 'completed') {
                            indicator.innerHTML = '✓';
                        } else if (status === 'problem') {
                            indicator.innerHTML = '⚠️';
                        } else {
                            indicator.innerHTML = '○';
                        }
                        
                        indicator.onclick = (e) => {
                            e.stopPropagation();
                            handleStatusClick(order.id, index, status);
                        };
                    }
                    
                    container.appendChild(indicator);
                    
                    // Add timestamp display below the indicator
                    if (order.stageTimestamps && order.stageTimestamps[index]) {
                        const timeDiv = document.createElement('div');
                        timeDiv.className = 'status-time';
                        timeDiv.textContent = formatDateTime(order.stageTimestamps[index]);
                        container.appendChild(timeDiv);
                    }
                    
                    cell.appendChild(container);
                    row.appendChild(cell);
                });
                
                tbody.appendChild(row);
            });
            
            updateOrdersCount();
        }

        function shouldStageBeDisabled(orderType, stageIndex) {
            const stageNames = ['new', 'cutting', 'edging', 'cnc', 'sanding', 'priming', 'painting', 'filming', 'drilling', 'assembly', 'quality', 'packing', 'ready'];
            const stageName = stageNames[stageIndex];
            
            if (orderType === 'painted') {
                return stageName === 'filming';
            } else if (orderType === 'film') {
                return stageName === 'priming' || stageName === 'painting';
            }
            
            return false;
        }

        // Status handling
        function handleStatusClick(orderId, stageIndex, currentStatus) {
            const orderIndex = orders.findIndex(o => o.id === orderId);
            const order = orders[orderIndex];
            
            if (currentStatus === 'pending') {
                const choice = confirm('Stage completed successfully?\n\nOK - Complete stage\nCancel - Mark problem');
                
                if (choice) {
                    order.stages[stageIndex] = 'completed';
                    
                    // Add timestamp
                    if (!order.stageTimestamps) order.stageTimestamps = {};
                    order.stageTimestamps[stageIndex] = new Date().toISOString();
                    
                    addToHistory(orderId, `Stage completed: ${STAGES[stageIndex]}`, STAGES[stageIndex]);
                    showNotification(t('step_completed'));
                    renderOrders();
                    saveDataToStorage();
                } else {
                    currentProblemOrderId = orderId;
                    currentProblemStageIndex = stageIndex;
                    showModal('problemModal');
                }
            } else if (currentStatus === 'problem') {
                if (currentUser.role === 'admin' || confirm('Problem resolved? Return stage to work?')) {
                    order.stages[stageIndex] = 'pending';
                    
                    // Remove timestamp
                    if (order.stageTimestamps && order.stageTimestamps[stageIndex]) {
                        delete order.stageTimestamps[stageIndex];
                    }
                    
                    addToHistory(orderId, `Problem resolved: ${STAGES[stageIndex]}`, STAGES[stageIndex]);
                    showNotification(t('problem_resolved'));
                    renderOrders();
                    saveDataToStorage();
                }
            } else if (currentStatus === 'completed') {
                // Only administrators can undo completed stages
                if (currentUser.role !== 'admin') {
                    showNotification(t('admin_required'), 'error');
                    return;
                }
                
                if (confirm('Return stage to work? (Administrator action)')) {
                    order.stages[stageIndex] = 'pending';
                    
                    // Remove timestamp
                    if (order.stageTimestamps && order.stageTimestamps[stageIndex]) {
                        delete order.stageTimestamps[stageIndex];
                    }
                    
                    addToHistory(orderId, `Stage returned to work by admin: ${STAGES[stageIndex]}`, STAGES[stageIndex]);
                    showNotification(t('step_returned'));
                    renderOrders();
                    saveDataToStorage();
                }
            }
        }

        function confirmProblem() {
            const comment = document.getElementById('problemComment')?.value || '';
            const orderIndex = orders.findIndex(o => o.id === currentProblemOrderId);
            
            if (orderIndex !== -1) {
                const order = orders[orderIndex];
                order.stages[currentProblemStageIndex] = 'problem';
                
                // Add timestamp for problem
                if (!order.stageTimestamps) order.stageTimestamps = {};
                order.stageTimestamps[currentProblemStageIndex] = new Date().toISOString();
                
                const problemText = comment ? 
                    `Problem: ${comment}` : 
                    `Problem at stage: ${STAGES[currentProblemStageIndex]}`;
                
                addToHistory(currentProblemOrderId, problemText, STAGES[currentProblemStageIndex]);
            }
            
            closeProblemModal();
            renderOrders();
            saveDataToStorage();
            showNotification(t('problem_marked'), 'error');
        }

        function closeProblemModal() {
            hideModal('problemModal');
            const problemComment = document.getElementById('problemComment');
            if (problemComment) problemComment.value = '';
            currentProblemOrderId = null;
            currentProblemStageIndex = null;
        }

        // Modal management
        function showModal(modalId) {
            const modal = document.getElementById(modalId);
            if (modal) {
                modal.style.display = 'block';
            }
        }

        function hideModal(modalId) {
            const modal = document.getElementById(modalId);
            if (modal) {
                modal.style.display = 'none';
            }
        }

        // Utility functions
        function addToHistory(orderId, action, stage) {
            const orderIndex = orders.findIndex(o => o.id === orderId);
            if (orderIndex !== -1) {
                orders[orderIndex].history.push({
                    time: new Date(),
                    user: currentUser.name,
                    action: action,
                    stage: stage
                });
            }
        }

        function getFilteredOrders() {
            const searchBox = document.getElementById('searchBox');
            const priorityFilter = document.getElementById('filterPriority');
            const statusFilter = document.getElementById('filterStatus');
            const typeFilter = document.getElementById('filterType');
            
            const searchTerm = searchBox ? searchBox.value.toLowerCase() : '';
            const priorityFilterValue = priorityFilter ? priorityFilter.value : '';
            const statusFilterValue = statusFilter ? statusFilter.value : '';
            const typeFilterValue = typeFilter ? typeFilter.value : '';

            // First filter by current month
            const monthOrders = getFilteredOrdersByMonth();

            return monthOrders.filter(order => {
                const matchesSearch = !searchTerm || 
                    order.id.toLowerCase().includes(searchTerm) || 
                    order.name.toLowerCase().includes(searchTerm) ||
                    order.clientName.toLowerCase().includes(searchTerm);

                const matchesPriority = !priorityFilterValue || order.priority === priorityFilterValue;
                const matchesType = !typeFilterValue || order.type === typeFilterValue;

                let matchesStatus = true;
                if (statusFilterValue) {
                    if (statusFilterValue === 'active') {
                        matchesStatus = !order.stages.every(s => s === 'completed') && !order.stages.includes('problem');
                    } else if (statusFilterValue === 'completed') {
                        matchesStatus = order.stages.every(s => s === 'completed');
                    } else if (statusFilterValue === 'problems') {
                        matchesStatus = order.stages.includes('problem');
                    }
                }

                return matchesSearch && matchesPriority && matchesStatus && matchesType;
            });
        }

        function formatDate(dateString) {
            if (!dateString) return '';
            return new Date(dateString).toLocaleDateString(currentLanguage === 'ru' ? 'ru-RU' : currentLanguage === 'ky' ? 'ru-RU' : 'en-US');
        }

        function formatDateTime(dateTimeString) {
            if (!dateTimeString) return '';
            const date = new Date(dateTimeString);
            const now = new Date();
            const isToday = date.toDateString() === now.toDateString();
            
            if (isToday) {
                // If today, show only time
                return date.toLocaleTimeString(currentLanguage === 'ru' ? 'ru-RU' : currentLanguage === 'ky' ? 'ru-RU' : 'en-US', {
                    hour: '2-digit',
                    minute: '2-digit'
                });
            } else {
                // If not today, show date and time
                const timeStr = date.toLocaleTimeString(currentLanguage === 'ru' ? 'ru-RU' : currentLanguage === 'ky' ? 'ru-RU' : 'en-US', {
                    hour: '2-digit',
                    minute: '2-digit'
                });
                const dateStr = date.toLocaleDateString(currentLanguage === 'ru' ? 'ru-RU' : currentLanguage === 'ky' ? 'ru-RU' : 'en-US', {
                    month: '2-digit',
                    day: '2-digit'
                });
                return `${dateStr} ${timeStr}`;
            }
        }

        function formatFileSize(bytes) {
            const sizes = ['B', 'KB', 'MB', 'GB'];
            if (bytes === 0) return '0 B';
            const i = Math.floor(Math.log(bytes) / Math.log(1024));
            return Math.round(bytes / Math.pow(1024, i) * 100) / 100 + ' ' + sizes[i];
        }

        function getDaysRemaining(deadline) {
            if (!deadline) return 0;
            const today = new Date();
            const deadlineDate = new Date(deadline);
            const diffTime = deadlineDate - today;
            const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24));
            return diffDays;
        }

        function showNotification(message, type = 'success') {
            const notification = document.getElementById('notification');
            if (notification) {
                notification.textContent = message;
                notification.className = `notification ${type}`;
                notification.classList.add('show');
                
                setTimeout(() => {
                    notification.classList.remove('show');
                }, 4000);
            }
        }

        // Search and filter
        function searchOrders() {
            renderOrders();
        }

        function filterOrders() {
            renderOrders();
        }

        // Export/Import
        function exportData() {
            const dataToExport = {
                orders: orders,
                exportDate: new Date().toISOString(),
                version: "5.0"
            };
            
            const dataStr = JSON.stringify(dataToExport, null, 2);
            const dataBlob = new Blob([dataStr], {type: 'application/json'});
            
            const link = document.createElement('a');
            link.href = URL.createObjectURL(dataBlob);
            link.download = `furniture_orders_${new Date().toISOString().split('T')[0]}.json`;
            link.click();
            
            showNotification(t('data_exported'));
        }

        function importData() {
            document.getElementById('importInput').click();
        }

        function handleImport(event) {
            const file = event.target.files[0];
            if (!file) return;

            const reader = new FileReader();
            reader.onload = function(e) {
                try {
                    const importedData = JSON.parse(e.target.result);
                    if (importedData.orders && Array.isArray(importedData.orders)) {
                        if (confirm('Import data? This will replace current data.')) {
                            orders = importedData.orders;
                            renderOrders();
                            saveDataToStorage();
                            showNotification(t('data_imported'));
                        }
                    } else {
                        showNotification(t('invalid_file'), 'error');
                    }
                } catch (error) {
                    showNotification(t('file_error'), 'error');
                }
            };
            reader.readAsText(file);
        }

        // Order details
        function openOrderDetails(orderId) {
            showNotification('🚧 Order details will be added in next version');
        }

        // Statistics
        function showStats() {
            showNotification('📊 Statistics will be added in next version');
        }

        // System functions
        function logout() {
            if (confirm('Are you sure you want to logout?')) {
                showNotification(t('goodbye'));
            }
        }

        // Click outside modal to close
        window.onclick = function(event) {
            if (event.target.classList.contains('modal')) {
                // Close specific modals
                if (event.target.id === 'materialsModal') {
                    closeMaterialsModal();
                } else {
                    event.target.style.display = 'none';
                }
            }
        }

        // Demo role switching (for demonstration purposes)
        setTimeout(() => {
            const controls = document.querySelector('.controls-grid');
            if (controls) {
                const demoDiv = document.createElement('div');
                demoDiv.innerHTML = `
                    <div style="grid-column: 1/-1; display: flex; gap: 0.75rem; align-items: center; justify-content: center; padding: 1.5rem; background: var(--background-color); border: 1px solid var(--border-color); border-radius: 0.375rem; margin-top: 1.5rem;">
                        <span style="color: var(--text-secondary); font-size: 0.875rem; font-weight: 500;">Demo Roles:</span>
                        <button class="btn btn-secondary" onclick="switchRole('worker')" style="padding: 0.5rem 1rem; font-size: 0.75rem;">👷‍♂️ Worker</button>
                        <button class="btn btn-secondary" onclick="switchRole('admin')" style="padding: 0.5rem 1rem; font-size: 0.75rem;">👨‍💼 Admin</button>
                        <button class="btn btn-secondary" onclick="switchRole('manager')" style="padding: 0.5rem 1rem; font-size: 0.75rem;">📊 Manager</button>
                    </div>
                `;
                controls.appendChild(demoDiv);
            }
        }, 2000);

        function switchRole(role) {
            currentUser.role = role;
            setupUserInterface();
            updateTranslations();
            showNotification(`🔄 Role changed: ${t('role_' + role)}`);
        }
    </script>
</body>
</html>
