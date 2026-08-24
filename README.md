html<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quadro de Tarefas - Guilherme & Manuella</title>
    <style>
        :root {
            --bg-color: #f0effc;
            --primary-color: #6c5ce7;
            --secondary-color: #a29bfe;
            --success-color: #00b894;
            --danger-color: #d63031;
            --warning-color: #fdcb6e;
            --text-color: #2d3436;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Comic Sans MS', 'Chalkboard SE', 'Ubuntu', sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-color);
            padding: 20px 10px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .container {
            width: 100%;
            max-width: 600px;
            background: white;
            padding: 25px 20px;
            border-radius: 30px;
            box-shadow: 0 10px 0px rgba(108, 92, 231, 0.15);
            border: 4px solid var(--primary-color);
        }

        h1 {
            text-align: center;
            color: var(--primary-color);
            font-size: 28px;
            margin-bottom: 5px;
            text-shadow: 2px 2px 0px var(--secondary-color);
        }

        .subtitle {
            text-align: center;
            font-size: 18px;
            color: #636e72;
            margin-bottom: 25px;
            font-weight: bold;
        }

        /* Top Bar Menu */
        .top-menu {
            display: flex;
            justify-content: space-between;
            background: #f1f2f6;
            padding: 10px;
            border-radius: 20px;
            margin-bottom: 20px;
            font-size: 13px;
            font-weight: bold;
        }

        .menu-btn {
            background: none;
            border: none;
            cursor: pointer;
            color: var(--primary-color);
            display: flex;
            align-items: center;
            gap: 5px;
        }

        /* Scoreboard Game Style */
        .scoreboard {
            background: linear-gradient(135deg, var(--primary-color), #81ecec);
            color: white;
            border-radius: 25px;
            padding: 20px;
            text-align: center;
            margin-bottom: 25px;
            box-shadow: inset 0 -5px 0px rgba(0,0,0,0.2), 0 5px 15px rgba(108, 92, 231, 0.4);
            position: relative;
            overflow: hidden;
        }

        .scoreboard::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(255,255,255,0.15) 10%, transparent 20%);
            background-size: 20px 20px;
        }

        .scoreboard-title {
            font-size: 16px;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 5px;
            opacity: 0.9;
        }

        .balance-value {
            font-size: 42px;
            font-weight: 900;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            text-shadow: 3px 3px 0px rgba(0,0,0,0.2);
        }

        .coin-animation {
            animation: bounce 0.6s infinite alternate ease-in-out;
        }

        @keyframes bounce {
            from { transform: translateY(0); }
            to { transform: translateY(-8px); }
        }

        /* Backup Alert Box */
        .alert-box {
            background-color: #ffeaa7;
            border: 3px dashed var(--warning-color);
            padding: 12px;
            border-radius: 20px;
            font-size: 14px;
            text-align: center;
            margin-bottom: 25px;
            display: none;
            font-weight: bold;
        }

        /* Task Cards */
        .task-list {
            display: flex;
            flex-direction: column;
            gap: 15px;
            margin-bottom: 25px;
        }

        .task-card {
            background: #f9f9ff;
            border: 3px solid #e4e4ee;
            border-radius: 20px;
            padding: 15px;
            display: flex;
            flex-direction: column;
            gap: 12px;
            transition: all 0.2s;
        }

        .task-card.done {
            border-color: var(--success-color);
            background-color: #e8fcf7;
        }

        .task-card.failed {
            border-color: var(--danger-color);
            background-color: #ffeef0;
        }

        .task-card.free {
            border-color: var(--warning-color);
            background-color: #fffdf0;
        }

        .task-title {
            font-size: 18px;
            font-weight: bold;
            color: var(--text-color);
        }

        /* Big Game Buttons */
        .btn-group {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 8px;
        }

        .action-btn {
            border: none;
            padding: 12px 5px;
            border-radius: 15px;
            font-size: 14px;
            font-weight: bold;
            cursor: pointer;
            color: white;
            transition: transform 0.1s, box-shadow 0.1s;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            gap: 4px;
        }

        .action-btn:active {
            transform: translateY(3px);
            box-shadow: none !important;
        }

        .btn-done {
            background-color: var(--success-color);
            box-shadow: 0 4px 0px #009477;
        }

        .btn-failed {
            background-color: var(--danger-color);
            box-shadow: 0 4px 0px #b32424;
        }

        .btn-free {
            background-color: var(--warning-color);
            color: #7f5f00;
            box-shadow: 0 4px 0px #d5ab3c;
        }

        /* Active State of Action Buttons */
        .task-card.done .btn-done { background-color: #009477; box-shadow: inset 0 4px 4px rgba(0,0,0,0.2); }
        .task-card.failed .btn-failed { background-color: #b32424; box-shadow: inset 0 4px 4px rgba(0,0,0,0.2); }
        .task-card.free .btn-free { background-color: #d5ab3c; box-shadow: inset 0 4px 4px rgba(0,0,0,0.2); }

        /* Backup Actions Footer */
        .backup-zone {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin-top: 20px;
            border-top: 3px dashed #e4e4ee;
            padding-top: 20px;
        }

        .btn-backup {
            background: #74b9ff;
            color: white;
            border: none;
            padding: 12px;
            border-radius: 15px;
            font-weight: bold;
            cursor: pointer;
            box-shadow: 0 4px 0px #4a90e2;
            text-align: center;
            font-size: 14px;
        }
        
        .btn-backup-import {
            background: #a29bfe;
            box-shadow: 0 4px 0px #7467ef;
        }

        .btn-backup:active {
            transform: translateY(3px);
            box-shadow: none;
        }

        #file-input {
            display: none;
        }
    </style>
</head>
<body>

    <div class="container">
        <!-- Top Menu Items -->
        <div class="top-menu">
            <button class="menu-btn" onclick="alert('Funcionalidade de visualização em desenvolvimento!')">🔒 Modo Visualização</button>
            <button class="menu-btn" onclick="alert('Resumo mensal indisponível no protótipo básico.')">📅 Resumo Mensal</button>
            <button class="menu-btn" onclick="changePin()">🔑 Trocar PIN</button>
        </div>

        <h1>Quadro de Tarefas</h1>
        <div class="subtitle">✨ Guilherme & Manuella ✨</div>

        <!-- Scoreboard placar de moedas -->
        <div class="scoreboard">
            <div class="scoreboard-title">💰 Saldo Acumulado</div>
            <div class="balance-value">
                <span class="coin-animation">💰</span>
                <span id="balance-amount">R$ 0,00</span>
            </div>
        </div>

        <!-- Auto-save error indicator alert -->
        <div class="alert-box" id="save-alert">
            ⚠ Salvamento em nuvem falhou! Por segurança, use "Baixar Backup" antes de fechar a página.
        </div>

        <!-- Task List Area -->
        <div class="task-list" id="tasks-container">
            <!-- As tarefas serão carregadas aqui dinamicamente pelo JavaScript -->
        </div>

        <!-- System Backup Management Operations -->
        <div class="backup-zone">
            <button class="btn-backup" onclick="exportBackup()">⬇ Baixar Backup</button>
            <button class="btn-backup btn-backup-import" onclick="document.getElementById('file-input').click()">⬆ Importar Backup</button>
            <input type="file" id="file-input" accept=".json" onchange="importBackup(event)">
        </div>
    </div>

    <script>
        // Configuração inicial de recompensas e tarefas padrão
        const REWARDS = { done: 0.50, failed: -1.00, free: 0.00 };
        const DEFAULT_TASKS = [
            { id: 1, title: "Arrumar a cama ao acordar 🛏" },
            { id: 2, title: "Escovar os dentes após as refeições 🪥" },
            { id: 3, title: "Fazer a lição de casa com capricho 📚" },
            { id: 4, title: "Organizar e guardar os brinquedos 🧸" },
            { id: 5, title: "Ajudar a tirar a mesa do jantar 🍽" }
        ];

        let appData = {
            balance: 0.00,
            taskStates: {}, // Armazena o estado atual de cada tarefa (done, failed, free)
            pin: "1234"
        };

        // Inicializador do Sistema
        window.onload = function() {
