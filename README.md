<!DOCTYPE html>
<html lang="pt-PT">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Comando Central - Vantal Frota 🕹️</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Share+Tech+Mono&display=swap');

        :root {
            --bg-color: #050505; --panel-bg: #111; --neon-blue: #00f3ff;
            --neon-purple: #bc13fe; --neon-green: #39ff14; --neon-red: #ff003c;
            --text-color: #e0e0e0;
        }

        body {
            background-color: var(--bg-color); color: var(--text-color);
            font-family: 'Share Tech Mono', monospace; margin: 0; padding: 20px;
            background-image: linear-gradient(rgba(0, 243, 255, 0.03) 1px, transparent 1px),
                              linear-gradient(90deg, rgba(0, 243, 255, 0.03) 1px, transparent 1px);
            background-size: 40px 40px;
        }

        h1 {
            text-align: center; color: var(--neon-blue); text-shadow: 0 0 10px var(--neon-blue);
            text-transform: uppercase; margin-bottom: 20px;
        }

        .hud-container {
            max-width: 1400px; margin: 0 auto; background-color: var(--panel-bg);
            border: 2px solid var(--neon-blue); padding: 25px; border-radius: 10px;
            box-shadow: 0 0 15px rgba(0, 243, 255, 0.2);
        }

        .controls { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; margin-bottom: 15px; }
        .input-group { display: flex; flex-direction: column; gap: 5px; }
        .input-group label { color: var(--neon-purple); font-size: 14px; text-transform: uppercase; }

        input, select {
            background-color: #000; color: var(--neon-green); border: 1px solid var(--neon-purple);
            padding: 10px; font-family: 'Share Tech Mono', monospace; font-size: 16px; outline: none;
            color-scheme: dark;
        }

        button.btn-principal {
            background-color: rgba(57, 255, 20, 0.1); color: var(--neon-green); border: 2px solid var(--neon-green);
            padding: 12px; font-family: 'Share Tech Mono', monospace; font-size: 18px; cursor: pointer;
            text-transform: uppercase; font-weight: bold; grid-column: 1 / -1; margin-top: 5px;
            transition: 0.3s;
        }
        button.btn-principal:hover { background-color: var(--neon-green); color: #000; box-shadow: 0 0 15px var(--neon-green); }

        .table-container {
            width: 100%; max-height: 50vh; overflow-y: auto; overflow-x: auto;
            border: 1px solid #333; margin-bottom: 20px; background-color: #0a0a0a;
        }

        table { width: 100%; border-collapse: collapse; }
        th, td { border: 1px solid #222; padding: 12px; text-align: center; white-space: nowrap; font-size: 14px; }
        th { background-color: #001f22; color: var(--neon-blue); position: sticky; top: 0; z-index: 10; box-shadow: 0 2px 5px rgba(0,0,0,0.8); }
        tr:hover { background-color: rgba(0, 243, 255, 0.1); }
        
        .status-nao-pago { color: var(--neon-red); font-weight: bold; font-size: 15px; }
        .status-pago { color: var(--neon-green); font-weight: bold; font-size: 15px; }

        .btn-acao { 
            background: #000; color: var(--neon-green); border: 1px solid var(--neon-green); 
            padding: 6px 10px; cursor: pointer; font-size: 12px; margin-top: 5px; border-radius: 4px; font-family: 'Share Tech Mono';
        }
        .btn-acao:hover { background: var(--neon-green); color: #000; }
        .btn-acao.reversao { color: var(--neon-red); border-color: var(--neon-red); }
        .btn-acao.reversao:hover { background: var(--neon-red); color: #000; }

        /* Novo Botão de Lápis para Edição */
        .btn-edit {
            background: transparent; border: none; cursor: pointer; font-size: 14px;
            margin-left: 8px; opacity: 0.5; transition: 0.3s;
        }
        .btn-edit:hover { opacity: 1; transform: scale(1.3); }

        .terminal {
            background: #000; color: #39ff14; font-family: monospace; padding: 15px;
            border: 1px solid #333; height: 100px; overflow-y: auto; font-size: 14px;
        }
    </style>
</head>
<body>

    <h1>[ SISTEMA OPERACIONAL VANTAL ]</h1>

    <div class="hud-container">
        <div class="controls">
            <div class="input-group">
                <label>Unidade Móvel</label>
                <select id="abaPlanilha">
                    <option value="24280-OSQ7J73">🚚 VW 24.280 (OSQ7J73)</option>
                    <option value="Darf-CFSBJ-6B18">🚚 DAF CF 330</option>
                    <option value="Vendas">📦 Vendas</option>
                    <option value="Comissoes">💰 Comissões</option>
                </select>
            </div>
            <div class="input-group">
                <label>Status Financeiro</label>
                <select id="filtroStatus">
                    <option value="TODOS">⚠️ Mostrar Todos</option>
                    <option value="PAGO">✅ Apenas Pagos</option>
                    <option value="NAO_PAGO">🔴 Apenas Não Pagos / Pendentes</option>
                </select>
            </div>
            <div class="input-group">
                <label>Data Inicial</label><input type="date" id="dataInicial">
            </div>
            <div class="input-group">
                <label>Data Final</label><input type="date" id="dataFinal">
            </div>
            <div class="input-group">
                <label>Palavra-chave</label><input type="text" id="termoBusca" placeholder="Ex: Areia, Barro...">
            </div>
            
            <button class="btn-principal" onclick="carregarDados()">⚙️ EXECUTAR VARREDURA</button>
        </div>

        <div class="table-container">
            <table id="tabelaResultados">
                <thead id="cabecalhoTabela"></thead>
                <tbody id="corpoTabela"></tbody>
            </table>
        </div>

        <h3 style="color: var(--neon-purple); margin-bottom: 5px; font-size: 14px;">[ LOG DO SISTEMA ]</h3>
        <div id="terminalLog" class="terminal">
            A aguardar comando de varredura...<br>
        </div>
    </div>

    <script>
        const URL_WEB_APP = "https://script.google.com/macros/s/AKfycbwQo8vVecdGHmirrQkXcp6mts0MFLk_KE_bOiTE51ln529feFFc-7bNFgnZVeDqgp8/exec";
        const ID_PLANILHA = "17ZabKZfm5HjiEvMmogjus6ZSmA8vS_6V8GXetSkJMY4";

        function log(msg, cor = "#39ff14") {
            const term = document.getElementById("terminalLog");
            const hora = new Date().toLocaleTimeString();
            term.innerHTML += `<span style="color:${cor}">[${hora}] ${msg}</span><br>`;
            term.scrollTop = term.scrollHeight;
        }

        function indiceParaColuna(index) {
            let letter = '';
            let temp = index + 1;
            while (temp > 0) {
                let mod = (temp - 1) % 26;
                letter = String.fromCharCode(65 + mod) + letter;
                temp = Math.floor((temp - mod) / 26);
            }
            return letter;
        }

        async function carregarDados() {
            const aba = document.getElementById("abaPlanilha").value;
            const termoBusca = document.getElementById("termoBusca").value.toLowerCase();
            const dataInicialStr = document.getElementById("dataInicial").value;
            const dataFinalStr = document.getElementById("dataFinal").value;
            const filtroStatusValor = document.getElementById("filtroStatus").value;
            
            const thead = document.getElementById("cabecalhoTabela");
            const tbody = document.getElementById("corpoTabela");

            thead.innerHTML = "";
            tbody.innerHTML = "";
            log(`A carregar base de dados: "${aba}"...`, "#00f3ff");

            try {
                const urlConsulta = `${URL_WEB_APP}?ID=${ID_PLANILHA}&SH=${aba}&FN=readSheet`;
                const resposta = await fetch(urlConsulta);
                const textoPuro = await resposta.text();
                
                let dados;
                try { dados = JSON.parse(textoPuro); } catch (e) { log("ERRO: O Google bloqueou o acesso.", "red"); return; }

                if (!dados || dados.length === 0) return;

                let indiceCabecalho = -1;
                for (let i = 0; i < Math.min(15, dados.length); i++) {
                    let primeiraCelula = String(dados[i][0]).toUpperCase().trim();
                    if (primeiraCelula === "ID" || primeiraCelula.includes("DATA")) {
                        indiceCabecalho = i;
                        break;
                    }
                }

                if (indiceCabecalho === -1) { log("Erro: Cabeçalho não encontrado.", "red"); return; }

                const cabecalho = dados[indiceCabecalho];
                const linhasDados = dados.slice(indiceCabecalho + 1);

                let indiceData = cabecalho.findIndex(col => String(col).toUpperCase().includes("DATA"));
                let indiceStatus = cabecalho.findIndex(col => String(col).toUpperCase().includes("STATUS"));

                let trCabecalho = "<tr>";
                cabecalho.forEach(coluna => { trCabecalho += `<th>${coluna || '-'}</th>`; });
                trCabecalho += "</tr>";
                thead.innerHTML = trCabecalho;

                let linhasAdicionadas = 0;

                linhasDados.forEach((linha, indexArray) => {
                    let linhaRealPlanilha = indiceCabecalho + 2 + indexArray; 
                    if (!linha[0] || String(linha[0]).trim() === "") return;

                    const linhaTexto = linha.join(" ").toLowerCase();
                    if (termoBusca && !linhaTexto.includes(termoBusca)) return;

                    if (indiceData !== -1 && (dataInicialStr || dataFinalStr)) {
                        let dataLinhaStr = String(linha[indiceData]); 
                        let partesData = dataLinhaStr.split("-");
                        if (partesData.length === 3) {
                            let dataComparacao = `${partesData[2]}-${partesData[1]}-${partesData[0]}`; 
                            if (dataInicialStr && dataComparacao < dataInicialStr) return;
                            if (dataFinalStr && dataComparacao > dataFinalStr) return;
                        }
                    }

                    let statusAtual = indiceStatus !== -1 ? String(linha[indiceStatus]).toLowerCase() : "";
                    let isPago = statusAtual.includes("pago") && !statusAtual.includes("não");
                    let isNaoPago = statusAtual.includes("não") || statusAtual.includes("pendente");

                    if (filtroStatusValor === "PAGO" && !isPago) return;
                    if (filtroStatusValor === "NAO_PAGO" && !isNaoPago) return;

                    let trDado = "<tr>";
                    linha.forEach((celula, indexColuna) => {
                        let conteudoTexto = celula || '';
                        let nomeColuna = String(cabecalho[indexColuna] || '').toUpperCase().trim();
                        let letraColuna = indiceParaColuna(indexColuna);
                        let celulaA1 = `${letraColuna}${linhaRealPlanilha}`; // Ex: C15
                        
                        let safeValorParaJavaScript = String(conteudoTexto).replace(/'/g, "\\'").replace(/"/g, "&quot;");

                        // LÓGICA DE GERAÇÃO DAS CÉLULAS
                        if (!nomeColuna || nomeColuna === "ID" || nomeColuna === "DATA DE CADASTRO") {
                            // Células bloqueadas para edição (ID e Data) ou Colunas Vazias
                            trDado += `<td>${conteudoTexto}</td>`;
                            
                        } else if (nomeColuna.includes("STATUS")) {
                            // Lógica do botão Pago/Não Pago
                            let conteudoStatus = "";
                            if (isNaoPago) {
                                conteudoStatus = `<span class="status-nao-pago">${conteudoTexto}</span>
                                            <br><button class="btn-acao" onclick="enviarEdicao('${aba}', '${celulaA1}', '🟢 Pago')">✅ MARCAR PAGO</button>`;
                            } else if (isPago) {
                                conteudoStatus = `<span class="status-pago">${conteudoTexto}</span>
                                            <br><button class="btn-acao reversao" onclick="enviarEdicao('${aba}', '${celulaA1}', '🔴 Não Pago')">❌ ESTORNAR</button>`;
                            } else {
                                conteudoStatus = conteudoTexto; // Caso o status esteja em branco ou diferente
                            }
                            trDado += `<td>${conteudoStatus}</td>`;
                            
                        } else {
                            // Célula NORMAL (Editável com Lápis)
                            trDado += `<td>${conteudoTexto} <button class="btn-edit" onclick="perguntarEdicao('${aba}', '${celulaA1}', '${nomeColuna}', '${safeValorParaJavaScript}')">✏️</button></td>`;
                        }
                    });
                    trDado += "</tr>";
                    
                    tbody.innerHTML += trDado;
                    linhasAdicionadas++;
                });

                log(`Tabela atualizada. ${linhasAdicionadas} registos encontrados.`);

            } catch (erro) {
                log(`Erro ao carregar dados: ${erro.message}`, "red");
            }
        }

        // FUNÇÃO QUE ABRE O POP-UP DE PERGUNTA PARA EDITAR O DADO
        function perguntarEdicao(aba, celulaRef, nomeColuna, valorAtual) {
            // Usa o prompt nativo do navegador para perguntar o novo valor
            let novoValor = prompt(`[EDIÇÃO DE DADOS]\nEstá a editar a coluna: ${nomeColuna}\nDigite o novo valor:`, valorAtual);
            
            // Se o utilizador clicar em cancelar, ou não mudar nada, a função para aqui
            if (novoValor === null) {
                log(`Edição cancelada pelo operador.`, "yellow");
                return; 
            }
            if (novoValor.trim() === valorAtual.trim()) {
                return;
            }

            // Se alterou algo, manda gravar na nuvem
            enviarEdicao(aba, celulaRef, novoValor);
        }

        // FUNÇÃO QUE DE FACTO COMUNICA COM O GOOGLE SHEETS
        async function enviarEdicao(aba, celulaRef, novoValor) {
            log(`A enviar nova informação (${novoValor}) para a célula ${celulaRef}...`, "yellow");
            
            const valorCodificado = encodeURIComponent(novoValor);
            const urlEdicao = `${URL_WEB_APP}?ID=${ID_PLANILHA}&SH=${aba}&FN=writeCell&REF=${celulaRef}&DATA=${valorCodificado}`;

            try {
                const resposta = await fetch(urlEdicao);
                await resposta.text();
                
                log(`Alteração gravada no servidor principal!`, "#39ff14");
                carregarDados(); // Recarrega a tabela para mostrar o valor alterado
            } catch (erro) {
                log(`Falha ao alterar dado. Tente de novo. Erro: ${erro.message}`, "red");
                alert("Falha na comunicação com o Google Sheets.");
            }
        }
    </script>
</body>
</html>
