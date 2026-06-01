# crispy-winner
Simulação Brasileiro 
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simulador Brasileirão 2026</title>
    <style>
        /* ==========================================
           1. VARIÁVEIS DE DESIGN & PALETA DE CORES
           ========================================== */
        :root {
            --bg-principal: #0d1117;
            --bg-card: #161b22;
            --bg-input: #21262d;
            --texto-principal: #c9d1d9;
            --texto-secundario: #8b949e;
            --verde-cbf: #00875a;
            --verde-brilho: #00ffaa;
            --amarelo-cbf: #fcf003;
            --azul-destaque: #1f6feb;
            --vermelho-rebaixamento: #da3637;
            --borda: #30363d;
            --libertadores: #0052cc;
            --sulamericana: #e67e22;
            --fonte: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        /* ==========================================
           2. RESET E CONFIGURAÇÕES GERAIS
           ========================================== */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: var(--fonte);
        }

        body {
            background-color: var(--bg-principal);
            color: var(--texto-principal);
            line-height: 1.6;
            padding-bottom: 60px;
        }

        header {
            background: linear-gradient(135deg, #052e16 0%, #022c22 100%);
            border-bottom: 4px solid var(--amarelo-cbf);
            padding: 20px;
            text-align: center;
            box-shadow: 0 4px 20px rgba(0,0,0,0.5);
        }

        header h1 {
            color: #ffffff;
            font-size: 2.2rem;
            text-shadow: 0 2px 4px rgba(0,0,0,0.6);
            letter-spacing: 1px;
        }

        header h1 span {
            color: var(--amarelo-cbf);
        }

        header p {
            color: var(--texto-secundario);
            font-size: 0.95rem;
            margin-top: 5px;
        }

        .container {
            width: 95%;
            max-width: 1400px;
            margin: 25px auto;
        }

        /* ==========================================
           3. NAVEGAÇÃO POR ABAS (SÉRIES)
           ========================================== */
        .abas-series {
            display: flex;
            gap: 10px;
            margin-bottom: 25px;
            overflow-x: auto;
            padding-bottom: 5px;
        }

        .aba-btn {
            background-color: var(--bg-card);
            color: var(--texto-principal);
            border: 1px solid var(--borda);
            padding: 12px 25px;
            font-size: 1.1rem;
            font-weight: bold;
            cursor: pointer;
            border-radius: 6px;
            transition: all 0.3s ease;
            white-space: nowrap;
        }

        .aba-btn:hover {
            border-color: var(--verde-brilho);
            background-color: #1f2937;
        }

        .aba-btn.ativa {
            background-color: var(--verde-cbf);
            color: #ffffff;
            border-color: var(--amarelo-cbf);
            box-shadow: 0 0 10px rgba(0, 135, 90, 0.4);
        }

        /* ==========================================
           4. LAYOUT PRINCIPAL (GRID DASHBOARD)
           ========================================== */
        .dashboard-grid {
            display: grid;
            grid-template-columns: 1fr;
            gap: 25px;
        }

        @media (min-width: 1024px) {
            .dashboard-grid {
                grid-template-columns: 2fr 1fr;
            }
        }

        .painel {
            background-color: var(--bg-card);
            border: 1px solid var(--borda);
            border-radius: 8px;
            padding: 20px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.3);
            margin-bottom: 25px;
        }

        .painel-titulo {
            font-size: 1.3rem;
            color: #ffffff;
            margin-bottom: 15px;
            border-left: 4px solid var(--verde-cbf);
            padding-left: 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        /* ==========================================
           5. ESTILIZAÇÃO DA TABELA DE CLASSIFICAÇÃO
           ========================================== */
        .tabela-container {
            overflow-x: auto;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            text-align: center;
            font-size: 0.95rem;
        }

        th {
            background-color: #0d1117;
            color: var(--texto-secundario);
            font-weight: 600;
            padding: 12px 8px;
            border-bottom: 2px solid var(--borda);
        }

        th.alinhado-esquerda, td.alinhado-esquerda {
            text-align: left;
            padding-left: 15px;
        }

        td {
            padding: 10px 8px;
            border-bottom: 1px solid var(--borda);
            color: var(--texto-principal);
        }

        tr:hover {
            background-color: #1f242c;
        }

        /* Cores das Zonas de Classificação */
        .zona-libertadores { border-left: 5px solid var(--libertadores); }
        .zona-sulamericana { border-left: 5px solid var(--sulamericana); }
        .zona-rebaixamento { border-left: 5px solid var(--vermelho-rebaixamento); }
        
        .posicao-num {
            font-weight: bold;
            display: inline-block;
            width: 24px;
        }

        .nome-clube {
            display: flex;
            align-items: center;
            gap: 10
            
