<!DOCTYPE html>
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
            max-width: 800px;
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

        /* Top Menu */
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

        /* Placar de Moedas */
        .scoreboard {
            background: linear-gradient(135deg, var(--primary-color), #81ecec);
            color: white;
            border-radius: 25px;
            padding: 15px;
            text-align: center;
            margin-bottom: 25px;
            box-shadow: inset 0 -5px 0px rgba(0,0,0,0.2), 0 5px 15px rgba(108, 92, 231, 0.4);
        }

        .scoreboard-title {
            font-size: 14px;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 5px;
            opacity: 0.9;
        }

        .balance-container {
            display: flex;
            justify-content: center;
            gap: 30px;
            align-items: center;
            flex-wrap: wrap;
        }

        .child-score {
            background: rgba(255, 255, 255, 0.2);
            padding: 10px 20px;
            border-radius: 15px;
            border: 2px solid rgba(255, 255, 255, 0.4);
        }

        .child-name {
            font-size: 16px;
            font-weight: bold;
        }

        .balance-value {
            font-size: 28px;
            font-weight: 900;
            text-shadow: 2px 2px 0px rgba(0,0,0,0.2);
        }

        /* Tabela Responsiva */
        .table-container {
            overflow-x: auto;
            margin-bottom: 25px;
            border-radius: 20px;
            border: 3px solid #e4e4ee;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            background: #f9f9ff;
            text-align: center;
        }

        th, td {
            padding: 12px 8px;
            border: 1px solid #e4e4ee;
            min-width: 50px;
        }

        th {
            background-color: #e8fcf7;
            color: var(--primary-color);
            font-weight: bold;
            font-size: 13px;
        }

        .task-row-title {
            text-align: left;
            font-weight: bold;
            font-size: 14px;
            color: var(--text-color);
            min-width: 150px;
        }

        .child-section-title {
            background-color: var(--secondary-color) !important;
            color: white !important;
            text-align: left;
            font-size: 16px;
            padding-left: 15px;
        }

        /* Botões de Célula Gamificados */
        .cell-btn {
            width: 36px;
            height: 36px;
            border-radius: 50%;
            border: 3px solid #cbd5e1;
            background: white;
            cursor: pointer;
            font-size: 16px;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            transition: all 0.1s;
            font-weight: bold;
        }

        .cell-btn:active {
            transform: scale(0.9);
        }

        /* Estados dos botões */
        .cell-btn.done {
            background-color: var(--success-color);
            border-color: #009477;
            color: white;
        }

        .cell-btn.failed {
            background-color: var(--danger-color);
            border-color: #b32424;
            color: white;
        }

        .cell-btn.free {
            background-color: var(--warning-color);
            border-color: #d5ab3c;
            color: #7f5f00;
        }

        /* Legenda */
        .legend {
            background: #f1f2f6;
            padding: 15px;
            border-radius: 20px;
            display: flex;
            justify-content: space-around;
            flex-wrap: wrap;
            gap: 10px;
            font-size: 13px;
            font-weight: bold;
            margin-bottom: 25px;
        }

        .legend-item {
            display: flex;
            align-items: center;
            gap: 5px;
        }

        /* Footer de Backup */
        .backup-zone {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
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
            <button class="menu-btn" onclick="alert('Modo visualização ativado para verificação rápida!')">🔒 Modo Visualização</button>
            <button class="menu-btn" onclick="alert('Resumo mensal consolidado.')">📅 Resumo Mensal</button>
            <button class="menu-btn" onclick="changePin()">🔑 Trocar PIN</button>
        </div>

        <h1>Quadro de Tarefas</h1>
        <div class="subtitle">✨ Controle Semanal ✨</div>

        <!-- Placar de Moedas Separado por Filho -->
        <div class="scoreboard">
            <div class="scoreboard-title">💰 Placar de Moedas da Semana</div>
            <div class="balance-container">
                <div class="child-score">
                    <div class="child-name">👦 Guilherme (8 anos)</div>
                    <div class="balance-value" id="bal-guilherme">R$ 0,00</div>
                </div>
                <div class="child-score">
                    <div class="child-name">👧 Manuella</div>
                    <div class="balance-value" id="bal-manuella">R$ 0,00</div>
                </div>
            </div>
        </div>

        <!-- Legenda explicativa -->
        <div class="legend">
            <div class="legend-item"><span class="cell-btn done" style="width:24px; height:24px; font-size:11px;">⭐</span> Feito (+R$0,50)</div>
            <div class="legend-item"><span class="cell-btn failed" style="width:24px; height:24px; font-size:11px;">✕</span> Não feito (-R$1,00)</div>
            <div class="legend-item"><span class="cell-btn free" style="width:24px; height:24px; font-size:11px;">L</span> Dia Livre</div>
        </div>

        <!-- Área da Tabela das Crianças -->
        <div class="table-container">
            <table>
                <thead>
                    <tr>
                        <th>TAREFA</th>
                        <th>DOM</th>
                        <th>SEG</th>
                        <th>TER</th>
                        <th>QUA</th>
                        <th>QUI</th>
                        <th>SEX</th>
                        <th>SÁB</th>
                    </tr>
                </thead>
                <tbody id="table-body">
                    <!-- Gerado dinamicamente via JS com os dados exatos do seu print -->
                </tbody>
            </table>
        </div>

        <!-- Gerenciamento de Backup físico -->
        <div class="backup-zone">
            <button class="btn-backup" onclick="exportBackup()">⬇ Baixar Backup</button>
            <button class="btn-backup btn-backup-import" onclick="document.getElementById('file-input').click()">⬆ Importar Backup</button>
            <input type="file" id="file-input" accept=".json" onchange="importBackup(event)">
        </div>
    </div>

    <script>
        const REWARDS = { done: 0.50, failed: -1.00, free: 0.00 };
        const DAYS = ['dom', 'seg', 'ter', 'qua', 'qui', 'sex', 'sab'];

        // Lista exata de tarefas extraídas da sua imagem
        const DATA_STRUCTURE = {
            guilherme: {
