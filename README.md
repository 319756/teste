[APLICATIVO WEB 01 VERSAO 07.html](https://github.com/user-attachments/files/22658524/APLICATIVO.WEB.01.VERSAO.07.html)
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vantal Construção</title>
    <link href="https://fonts.googleapis.com/css2?family=Fredoka+One&family=Open+Sans:wght@400;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        :root {
            --cor-fundo: linear-gradient(135deg, #6DD5FA, #2980B9);
            --cor-header: linear-gradient(135deg, #F7971E, #FFD200);
            --cor-primaria: #FF6B6B;
            --cor-app: #FFFFFF;
            --cor-card: #f8f9fa;
            --cor-texto: #333;
            --cor-texto-claro: #555;
            --cor-borda: #e9ecef;
            --sombra: 0 4px 20px rgba(0,0,0,0.1);
        }
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { 
            font-family: 'Open Sans', sans-serif; 
            background: var(--cor-fundo); 
            min-height: 100vh; 
            display: flex; 
            justify-content: center; 
            align-items: center; 
        }
        .app { 
            background: var(--cor-app); 
            width: 100%; 
            max-width: 500px; 
            height: 95vh; 
            max-height: 800px; 
            border-radius: 15px; 
            overflow: hidden; 
            box-shadow: var(--sombra); 
            display: flex; 
            flex-direction: column; 
        }
        .header { 
            background: var(--cor-header); 
            color: white; 
            padding: 20px; 
            text-align: center; 
            font-family: 'Fredoka One', cursive; 
            font-size: 1.5em;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.2);
        }
        .content { flex: 1; overflow-y: auto; padding: 20px; padding-bottom: 90px; }
        .section { display: none; }
        .section.active { display: block; }
        .form-title { 
            font-family: 'Fredoka One', cursive; 
            color: var(--cor-primaria); 
            font-size: 1.4em; 
            margin-bottom: 25px; 
            text-align: center; 
        }
        .field { margin-bottom: 15px; }
        .field label { display: block; font-weight: 600; margin-bottom: 5px; font-size: 0.9em; color: var(--cor-texto-claro); }
        .field input, .field select { 
            width: 100%; 
            padding: 12px; 
            border: 2px solid var(--cor-borda); 
            border-radius: 8px; 
            font-size: 0.95em; 
        }
        .field input:focus, .field select:focus { 
            outline: none; 
            border-color: var(--cor-primaria); 
            box-shadow: 0 0 0 3px rgba(255, 107, 107, 0.2);
        }
        .row { display: flex; gap: 15px; }
        .row .field { flex: 1; }
        .btn { 
            width: 100%; 
            padding: 15px; 
            border: none; 
            border-radius: 8px; 
            font-size: 1.1em; 
            font-weight: 700; 
            cursor: pointer; 
            margin-top: 10px; 
            font-family: 'Fredoka One', cursive;
            transition: transform 0.15s ease, box-shadow 0.2s ease, background-color 0.2s ease;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            display: flex;
            align-items: center;
            justify-content: center;
            min-height: 55px;
        }
        .btn:hover {
            box-shadow: 0 5px 15px rgba(0,0,0,0.15);
        }
        .btn:active {
            transform: scale(0.98);
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
        }
        .btn:disabled {
            cursor: not-allowed;
            background: #ccc !important;
            background-image: none !important;
        }
        .spinner {
            border: 4px solid rgba(255, 255, 255, 0.4);
            border-radius: 50%;
            border-top: 4px solid #ffffff;
            width: 24px;
            height: 24px;
            animation: spin 1s linear infinite;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        .btn-venda { background: linear-gradient(45deg, #EEA849, #F46B45); color: white; }
        .btn-abastecimento { background: linear-gradient(45deg, #43E695, #38F9D7); color: white; }
        .btn-comissao { background: linear-gradient(45deg, #7028E4, #E5B2CA); color: white; }
        .filter-bar { display: flex; gap: 10px; margin-bottom: 20px; align-items: flex-end; flex-wrap: wrap; }
        .filter-bar .field { flex: 1; min-width: 120px; }
        .filter-bar button { flex-shrink: 0; width: auto; padding: 10px 15px; margin-bottom: 15px; }
        .card { 
            background: var(--cor-card); 
            border-radius: 10px; 
            padding: 15px; 
            margin-bottom: 12px; 
            border-left: 5px solid var(--cor-primaria);
        }
        .card-header { display: flex; justify-content: space-between; margin-bottom: 10px; padding-bottom: 10px; border-bottom: 1px solid var(--cor-borda); }
        .card-title { font-weight: 700; color: var(--cor-primaria); font-size: 1.1em; }
        .card-date { color: #666; font-size: 0.85em; }
        .card-row { display: flex; justify-content: space-between; margin: 8px 0; font-size: 0.95em; }
        .card-label { color: var(--cor-texto-claro); font-weight: 600; }
        .card-actions { display: flex; gap: 10px; margin-top: 15px; border-top: 1px solid var(--cor-borda); padding-top: 10px; }
        .card-actions button { flex: 1; padding: 8px; font-size: 0.8em; border: none; border-radius: 5px; cursor: pointer; display: flex; align-items: center; justify-content: center; gap: 5px; }
        .btn-edit { background: #FFC107; color: white; }
        .btn-delete { background: #F44336; color: white; }
        .badge { display: inline-block; padding: 4px 12px; border-radius: 12px; font-size: 0.8em; font-weight: 700; text-transform: uppercase; }
        .badge-pago, .badge-entregue { background: #4CAF50; color: white; }
        .badge-pendente { background: #FF9800; color: white; }
        .nav { position: fixed; bottom: 0; left: 50%; transform: translateX(-50%); width: 100%; max-width: 500px; height: 70px; background: white; display: flex; box-shadow: 0 -2px 10px rgba(0,0,0,0.1); border-top-left-radius: 15px; border-top-right-radius: 15px;}
        .nav-item { flex: 1; display: flex; flex-direction: column; align-items: center; justify-content: center; cursor: pointer; color: #999; font-size: 0.7em; font-weight: 600; }
        .nav-item i { font-size: 1.8em; margin-bottom: 5px; }
        .nav-item.active { color: var(--cor-primaria); }
        .toast { position: fixed; bottom: 90px; left: 50%; transform: translateX(-50%); background: #4CAF50; color: white; padding: 12px 24px; border-radius: 8px; font-weight: 600; opacity: 0; transition: opacity 0.3s; z-index: 1000; box-shadow: 0 3px 10px rgba(0,0,0,0.2); }
        .toast.show { opacity: 1; }
        .toast.error { background: #F44336; }
        .consulta-selector { display: flex; border-bottom: 2px solid var(--cor-borda); margin-bottom: 20px; }
        .btn-selector { flex: 1; background: none; border: none; padding: 12px; font-size: 1em; font-weight: 600; color: #999; cursor: pointer; border-bottom: 3px solid transparent; }
        .btn-selector.active { color: var(--cor-primaria); border-bottom: 3px solid var(--cor-primaria); }
        .filter-container { margin-bottom: 20px; }
        .summary-card { background-color: #fffbe6; border-left: 5px solid #FFD700; }
        .summary-card .card-row span:last-child { font-weight: 700; font-size: 1.1em; color: #333; }
        @media (max-width: 500px) { .app { height: 100vh; max-height: none; border-radius: 0; } .nav { border-radius: 0;} }
    </style>
</head>
<body>
    <div class="app">
        <div class="header"><i class="fas fa-truck"></i> Vantal Construção</div>
        <div class="content">
            <div class="field">
                <label for="truck">Selecione o Caminhão</label>
                <select id="truck">
                    <option value="24280">Caminhão 24280</option>
                    <option value="daf330">Caminhão DAF 330</option>
                </select>
            </div>
            
            <div id="sec-vendas" class="section active">
                <h2 class="form-title" id="venda-form-title">Registro de Venda</h2>
                <form id="form-vendas">
                    <input type="hidden" id="v-row-number">
                    <input type="hidden" id="v-data-cadastro">
                    
                    <div class="field"><label>Data da Venda</label><input type="date" id="v-data" required></div>
                    <div class="row">
                        <div class="field"><label>Cidade</label><input type="text" id="v-cidade" required></div>
                        <div class="field"><label>Cliente</label><input type="text" id="v-cliente" required></div>
                    </div>
                    <div class="row">
                        <div class="field"><label>Valor Vendido</label><input type="number" id="v-valor" step="0.01" required></div>
                        <div class="field"><label>Material</label><input type="text" id="v-material" required></div>
                    </div>
                    <div class="row">
                        <div class="field"><label>Diesel Gasto</label><input type="number" id="v-diesel" step="0.01"></div>
                        <div class="field"><label>Carregamento</label><input type="number" id="v-carga" step="0.01"></div>
                    </div>
                    <div class="row">
                        <div class="field">
                            <label>Gasto Extra</label>
                            <input type="number" id="v-extra" step="0.01" value="0">
                        </div>
                        <div class="field">
                            <label>Descrição Despesas</label>
                            <input type="text" id="v-desc" value="Nada">
                        </div>
                    </div>
                    <div class="row">
                         <div class="field">
                              <label>Motorista</label>
                              <select id="v-motorista" required><option value="">Carregando...</option></select>
                         </div>
                         <div class="field">
                              <label>Valor da comissão</label>
                              <input type="number" id="v-comissao" step="0.01">
                         </div>
                    </div>
                    <div class="field">
                        <label>Status da Venda</label>
                        <select id="v-status-venda" required>
                            <option value="PENDENTE">PENDENTE</option>
                            <option value="PAGO">PAGO</option>
                            <option value="ENTREGUE">ENTREGUE</option>
                        </select>
                    </div>

                    <button type="submit" class="btn btn-venda" id="btn-gravar-venda">Gravar Venda</button>
                    <button type="button" class="btn" style="background: #777; margin-top: 8px; display: none;" id="btn-cancelar-edicao-venda">Cancelar Edição</button>
                </form>
            </div>
            
            <div id="sec-abastecimento" class="section">
                <h2 class="form-title" id="abast-form-title">Registro de Abastecimento</h2>
                <form id="form-abastecimento">
                    <input type="hidden" id="a-row-number">
                    <input type="hidden" id="a-data-cadastro">
                    <div class="field"><label>Data</label><input type="date" id="a-data" required></div>
                    <div class="field"><label>Local</label><input type="text" id="a-local" required></div>
                    <div class="row">
                        <div class="field"><label>Valor Pago</label><input type="number" id="a-valor" step="0.01" required></div>
                        <div class="field"><label>Litros</label><input type="number" id="a-litros" step="0.01" required></div>
                    </div>
                    <div class="field"><label>Valor por Litro</label><input type="number" id="a-preco" step="0.01" required></div>
                    <button type="submit" class="btn btn-abastecimento" id="btn-gravar-abast">Registrar</button>
                    <button type="button" class="btn" style="background: #777; margin-top: 8px; display: none;" id="btn-cancelar-edicao-abast">Cancelar Edição</button>
                </form>
            </div>
            
            <div id="sec-consultas" class="section">
                <div class="consulta-selector">
                    <button id="btn-select-entregues" class="btn-selector active">Entregues</button>
                    <button id="btn-select-abastecimentos" class="btn-selector">Abastecimentos</button>
                    <button id="btn-select-comissoes" class="btn-selector">Comissões</button>
                    <button id="btn-select-pagamentos" class="btn-selector">Pagamentos</button>
                </div>
                
                <div id="filtros-entregues" class="filter-container">
                    <div class="filter-bar">
                        <div class="field">
                            <label for="month-filter">Filtrar por Mês</label>
                            <select id="month-filter">
                                <option value="todos">Mês Atual</option>
                                <option value="1">Janeiro</option><option value="2">Fevereiro</option><option value="3">Março</option><option value="4">Abril</option><option value="5">Maio</option><option value="6">Junho</option><option value="7">Julho</option><option value="8">Agosto</option><option value="9">Setembro</option><option value="10">Outubro</option><option value="11">Novembro</option><option value="12">Dezembro</option>
                            </select>
                        </div>
                        <button id="btn-fetch-entregues" class="btn btn-venda">Buscar</button>
                    </div>
                </div>
                <div id="filtros-abastecimentos" class="filter-container" style="display: none;">
                    <div class="filter-bar">
                        <div class="field"><label for="abast-start-date">De:</label><input type="date" id="abast-start-date"></div>
                        <div class="field"><label for="abast-end-date">Até:</label><input type="date" id="abast-end-date"></div>
                        <button id="btn-fetch-abastecimentos" class="btn btn-abastecimento">Buscar</button>
                    </div>
                </div>
                <div id="filtros-comissoes" class="filter-container" style="display: none;">
                    <div class="filter-bar">
                        <div class="field"><label for="comissao-start-date">De:</label><input type="date" id="comissao-start-date"></div>
                        <div class="field"><label for="comissao-end-date">Até:</label><input type="date" id="comissao-end-date"></div>
                        <div class="field">
                            <label for="comissao-status-filter">Status</label>
                            <select id="comissao-status-filter">
                                <option value="TODAS">Todas</option>
                                <option value="PENDENTE">Pendentes</option>
                                <option value="PAGO">Pagas</option>
                            </select>
                        </div>
                        <div class="field">
                            <label for="comissao-vendedor-filter">Vendedor</label>
                            <select id="comissao-vendedor-filter">
                                <option value="TODOS">Todos</option>
                            </select>
                        </div>
                        <button id="btn-fetch-comissoes" class="btn btn-comissao">Buscar</button>
                    </div>
                </div>
                <div id="filtros-pagamentos" class="filter-container" style="display: none;">
                    <div class="filter-bar">
                        <div class="field"><label for="pagamento-start-date">De:</label><input type="date" id="pagamento-start-date"></div>
                        <div class="field"><label for="pagamento-end-date">Até:</label><input type="date" id="pagamento-end-date"></div>
                        <div class="field">
                            <label for="pagamento-status-filter">Status</label>
                            <select id="pagamento-status-filter">
                                <option value="TODAS">Todos</option>
                                <option value="PENDENTE">Pendentes</option>
                                <option value="PAGO">Pagos</option>
                            </select>
                        </div>
                        <button id="btn-fetch-pagamentos" class="btn" style="background: #6B4EEA; color: white;">Buscar</button>
                    </div>
                </div>
                
                <div id="summary-container"></div>
                <div id="list-consultas"></div>
            </div>

            <div id="sec-comissoes" class="section">
                 <h2 class="form-title" id="comissao-form-title">Registro de Comissão (Vendedor)</h2>
                 <form id="form-comissao">
                       <input type="hidden" id="c-row-number">
                       <input type="hidden" id="c-data-cadastro">
                       <div class="field"><label>Data</label><input type="date" id="c-data" required></div>
                       <div class="field"><label>Cliente</label><input type="text" id="c-cliente" required></div>
                       <div class="field"><label>Local</label><input type="text" id="c-local" required></div>
                       <div class="field"><label>Material Vendido</label><input type="text" id="c-material" required></div>
                       <div class="row">
                           <div class="field"><label>Valor Comissão</label><input type="number" id="c-valor" step="0.01" required></div>
                           <div class="field">
                               <label>Vendedor</label>
                               <select id="c-vendedor" required>
                                   <option value="">Carregando...</option>
                               </select>
                           </div>
                       </div>
                       <div class="field"><label>Status</label><select id="c-status" required><option value="PENDENTE">PENDENTE</option><option value="PAGO">PAGO</option></select></div>
                       <button type="submit" class="btn btn-comissao" id="btn-gravar-comissao">Registrar Comissão</button>
                       <button type="button" class="btn" style="background: #777; margin-top: 8px; display: none;" id="btn-cancelar-edicao-comissao">Cancelar Edição</button>
                 </form>
            </div>

            <div id="sec-pagamentos" class="section">
                <h2 class="form-title">Registro de Pagamento de Cliente</h2>
                <form id="form-pagamento">
                    <div class="field"><label>Data do Pagamento</label><input type="date" id="p-data" required></div>
                    <div class="field"><label>Nome do Cliente</label><input type="text" id="p-cliente" required></div>
                    <div class="field"><label>Valor Pago</label><input type="number" id="p-valor" step="0.01" required></div>
                    <div class="field">
                        <label>Status</label>
                        <select id="p-status" required>
                            <option value="PAGO">PAGO</option>
                            <option value="PENDENTE">PENDENTE</option>
                        </select>
                    </div>
                    <div class="field"><label>Observação (Opcional)</label><input type="text" id="p-obs"></div>
                    <button type="submit" class="btn" id="btn-registrar-pagamento" style="background: linear-gradient(45deg, #6B4EEA, #412994); color: white;">Registrar Pagamento</button>
                </form>
            </div>
        </div>

        <div class="nav">
            <div class="nav-item active" data-sec="vendas"><i class="fas fa-shopping-cart"></i><span>Vendas</span></div>
            <div class="nav-item" data-sec="abastecimento"><i class="fas fa-gas-pump"></i><span>Abastecer</span></div>
            <div class="nav-item" data-sec="consultas"><i class="fas fa-search"></i><span>Consultas</span></div>
            <div class="nav-item" data-sec="comissoes"><i class="fas fa-hand-holding-usd"></i><span>Comissão</span></div>
            <div class="nav-item" data-sec="pagamentos"><i class="fas fa-dollar-sign"></i><span>Pagamentos</span></div>
        </div>

        <div id="toast" class="toast"></div>
    </div>
    
    <script>
        const URL_24280 = 'https://script.google.com/macros/s/AKfycbwRybCbuVR-mlZZaQkyOhqM0A3l3c6v2s90FHNWImCIRFIEdRU8uTaab28b98yoWnsvPA/exec'; // Substitua pela sua URL de implantação
        const URL_DAF330 = 'https://script.google.com/macros/s/AKfycbzM3nP86UqFYSYdhPDOFhzkc1Ktu77wdB5bO13P6n7mfAqjB-q6j4j7kIVSI9sbQZKK/exec'; // Substitua pela sua URL de implantação

        function getCorrectUrl(actionType) {
            const centralActions = [
                'getVendas', 'venda', 'editVenda', 'deleteVenda',
                'getMotoristas',
                'getVendedores',
                'getComissoes', 'comissao', 'editComissao', 'deleteComissao',
                'getPagamentos', 'pagamento'
            ];
            if (centralActions.includes(actionType)) {
                return URL_24280;
            }
            const truckSelection = document.getElementById('truck').value;
            return truckSelection === '24280' ? URL_24280 : URL_DAF330;
        }

        function toast(msg, erro = false) {
            const t = document.getElementById('toast');
            t.textContent = msg;
            t.className = 'toast show' + (erro ? ' error' : '');
            setTimeout(() => t.className = 'toast', 3000);
        }

        function getNow() { return new Date().toISOString(); }
        
        function formatDateForInput(dateString) {
            if (!dateString) return '';
            return new Date(dateString).toISOString().split('T')[0];
        }

        function handleEditVendaClick(data) {
            document.getElementById('venda-form-title').textContent = 'Editando Venda';
            document.getElementById('btn-gravar-venda').textContent = 'Salvar Alterações';
            document.getElementById('btn-cancelar-edicao-venda').style.display = 'block';
            document.getElementById('v-row-number').value = data.rowNumber;
            document.getElementById('v-data-cadastro').value = data.dataCadastro;
            document.getElementById('v-data').value = formatDateForInput(data.dataVenda);
            document.getElementById('v-cidade').value = data.cidade;
            document.getElementById('v-cliente').value = data.cliente;
            document.getElementById('v-valor').value = data.valorVendido;
            document.getElementById('v-material').value = data.material;
            document.getElementById('v-diesel').value = data.valorDieselGasto;
            document.getElementById('v-carga').value = data.valorParaEncher;
            document.getElementById('v-extra').value = data.gastoExtra;
            document.getElementById('v-desc').value = data.descricaoDespesas;
            document.getElementById('v-motorista').value = data.motorista;
            document.getElementById('v-comissao').value = data.valorComissao;
            document.getElementById('v-status-venda').value = data.statusVenda;
            document.querySelector('.nav-item[data-sec="vendas"]').click();
            document.getElementById('v-data').focus();
        }

        async function handleDeleteVendaClick(data, btn) {
            if (!confirm(`Tem certeza que deseja apagar a venda para o cliente "${data.cliente}"?`)) { 
                return; 
            }
            btn.innerHTML = '<div class="spinner"></div>';
            btn.disabled = true;
            try {
                const payload = { type: 'deleteVenda', rowNumber: data.rowNumber, dataVenda: data.dataVenda };
                await fetch(getCorrectUrl('deleteVenda'), { method: 'POST', mode: 'no-cors', body: JSON.stringify(payload) });
                toast('Registro apagado com sucesso!');
                fetchEntregues();
            } catch(error) {
                toast(`Erro ao apagar: ${error.message}`, true);
                btn.innerHTML = '<i class="fas fa-trash"></i> Apagar';
                btn.disabled = false;
            }
        }
        
        function resetVendaForm() {
            document.getElementById('form-vendas').reset();
            document.getElementById('v-row-number').value = '';
            document.getElementById('v-data-cadastro').value = '';
            document.getElementById('venda-form-title').textContent = 'Registro de Venda';
            document.getElementById('btn-gravar-venda').innerHTML = 'Gravar Venda';
            document.getElementById('btn-cancelar-edicao-venda').style.display = 'none';
        }

        function handleEditAbastecimentoClick(data) {
            document.getElementById('abast-form-title').textContent = 'Editando Abastecimento';
            document.getElementById('btn-gravar-abast').textContent = 'Salvar Alterações';
            document.getElementById('btn-cancelar-edicao-abast').style.display = 'block';
            document.getElementById('a-row-number').value = data.rowNumber;
            document.getElementById('a-data-cadastro').value = data.dataCadastro;
            document.getElementById('a-data').value = formatDateForInput(data.data);
            document.getElementById('a-local').value = data.local;
            document.getElementById('a-valor').value = data.valorpago;
            document.getElementById('a-litros').value = data.litros;
            document.getElementById('a-preco').value = data.valorporlitro;
            document.querySelector('.nav-item[data-sec="abastecimento"]').click();
            document.getElementById('a-data').focus();
        }

        async function handleDeleteAbastecimentoClick(data, btn) {
            if (!confirm(`Tem certeza que deseja apagar o abastecimento em "${data.local}"?`)) {
                return;
            }
            btn.innerHTML = '<div class="spinner"></div>';
            btn.disabled = true;
            try {
                const payload = { type: 'deleteAbastecimento', rowNumber: data.rowNumber };
                await fetch(getCorrectUrl('deleteAbastecimento'), { method: 'POST', mode: 'no-cors', body: JSON.stringify(payload) });
                toast('Registro apagado com sucesso!');
                fetchAbastecimentos();
            } catch(error) {
                toast(`Erro ao apagar: ${error.message}`, true);
                btn.innerHTML = '<i class="fas fa-trash"></i> Apagar';
                btn.disabled = false;
            }
        }

        function resetAbastecimentoForm() {
            document.getElementById('form-abastecimento').reset();
            document.getElementById('a-row-number').value = '';
            document.getElementById('a-data-cadastro').value = '';
            document.getElementById('abast-form-title').textContent = 'Registro de Abastecimento';
            document.getElementById('btn-gravar-abast').innerHTML = 'Registrar';
            document.getElementById('btn-cancelar-edicao-abast').style.display = 'none';
        }

        function handleEditComissaoClick(data) {
            document.getElementById('comissao-form-title').textContent = 'Editando Comissão';
            document.getElementById('btn-gravar-comissao').textContent = 'Salvar Alterações';
            document.getElementById('btn-cancelar-edicao-comissao').style.display = 'block';
            document.getElementById('c-row-number').value = data.rowNumber;
            document.getElementById('c-data-cadastro').value = data.dataCadastro;
            document.getElementById('c-data').value = formatDateForInput(data.data);
            document.getElementById('c-cliente').value = data.cliente;
            document.getElementById('c-local').value = data.local;
            document.getElementById('c-material').value = data.material;
            document.getElementById('c-valor').value = data.valorcomissao;
            document.getElementById('c-vendedor').value = data.vendedor;
            document.getElementById('c-status').value = data.status;
            document.querySelector('.nav-item[data-sec="comissoes"]').click();
            document.getElementById('c-data').focus();
        }

        async function handleDeleteComissaoClick(data, btn) {
            if (!confirm(`Tem certeza que deseja apagar a comissão para "${data.cliente}"?`)) {
                return;
            }
            btn.innerHTML = '<div class="spinner"></div>';
            btn.disabled = true;
            try {
                const payload = { type: 'deleteComissao', rowNumber: data.rowNumber };
                await fetch(getCorrectUrl('deleteComissao'), { method: 'POST', mode: 'no-cors', body: JSON.stringify(payload) });
                toast('Registro apagado com sucesso!');
                fetchComissoes();
            } catch(error) {
                toast(`Erro ao apagar: ${error.message}`, true);
                btn.innerHTML = '<i class="fas fa-trash"></i> Apagar';
                btn.disabled = false;
            }
        }

        function resetComissaoForm() {
            document.getElementById('form-comissao').reset();
            document.getElementById('c-row-number').value = '';
            document.getElementById('c-data-cadastro').value = '';
            document.getElementById('comissao-form-title').textContent = 'Registro de Comissão (Vendedor)';
            document.getElementById('btn-gravar-comissao').innerHTML = 'Registrar Comissão';
            document.getElementById('btn-cancelar-edicao-comissao').style.display = 'none';
        }
        
        async function fetchEntregues() {
            try {
                let selectedMonth = document.getElementById('month-filter').value;
                if (selectedMonth === 'todos') { selectedMonth = new Date().getMonth() + 1; }
                const url = `${getCorrectUrl('getVendas')}?action=getVendas&month=${selectedMonth}`;
                const response = await fetch(url);
                if (!response.ok) throw new Error('Erro de rede.');
                const data = await response.json();
                if (data.error) throw new Error(data.error);
                const listContainer = document.getElementById('list-consultas');
                if (!data || data.length === 0) {
                    listContainer.innerHTML = '<p>Nenhuma entrega encontrada para este mês.</p>';
                    return;
                }
                listContainer.innerHTML = data.map(e => {
                    const dataVenda = new Date(e.dataVenda).toLocaleDateString('pt-BR', { timeZone: 'UTC' });
                    const valorVendido = parseFloat(e.valorVendido).toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' });
                    const statusClass = e.statusVenda ? e.statusVenda.toLowerCase() : 'pendente';
                    const vendaJson = JSON.stringify(e).replace(/"/g, '&quot;');
                    return `<div class="card">
                                <div class="card-header"><div class="card-title">${e.cliente}</div><div class="card-date">${dataVenda}</div></div>
                                <div class="card-row"><span class="card-label">Cidade:</span><span>${e.cidade}</span></div>
                                <div class="card-row"><span class="card-label">Motorista:</span><span>${e.motorista || '-'}</span></div>
                                <div class="card-row"><span class="card-label">Valor:</span><span>${valorVendido}</span></div>
                                <div class="card-row"><span class="card-label">Status:</span><span class="badge badge-${statusClass}">${e.statusVenda}</span></div>
                                <div class="card-actions">
                                   <button class="btn btn-edit" data-venda='${vendaJson}'><i class="fas fa-edit"></i> Editar</button>
                                   <button class="btn btn-delete" data-venda='${vendaJson}'><i class="fas fa-trash"></i> Apagar</button>
                                </div>
                            </div>`;
                }).join('');
            } catch (error) {
                document.getElementById('list-consultas').innerHTML = `<p style="color: red;">Erro: ${error.message}</p>`;
                toast('Erro ao buscar entregas', true);
            }
        }
        
        async function fetchMotoristas() {
            const selectMotorista = document.getElementById('v-motorista');
            selectMotorista.innerHTML = '<option value="">Carregando...</option>';
            try {
                const url = `${getCorrectUrl('getMotoristas')}?action=getMotoristas`;
                const response = await fetch(url);
                if (!response.ok) throw new Error('Erro de rede.');
                const data = await response.json();
                if (data.error) throw new Error(data.error);
                if (!Array.isArray(data)) throw new Error('Resposta do servidor inválida.');
                selectMotorista.innerHTML = '<option value="">Selecione um motorista</option>';
                data.forEach(nome => {
                    if(nome) {
                        const option = document.createElement('option');
                        option.value = nome;
                        option.textContent = nome;
                        selectMotorista.appendChild(option);
                    }
                });
            } catch (error) {
                selectMotorista.innerHTML = '<option value="">Erro ao carregar</option>';
                toast(`Erro motoristas: ${error.message}`, true);
            }
        }

        async function fetchVendedores() {
            const selectVendedorFiltro = document.getElementById('comissao-vendedor-filter');
            const selectVendedorForm = document.getElementById('c-vendedor');
            selectVendedorFiltro.innerHTML = '<option value="TODOS">Todos</option>';
            selectVendedorForm.innerHTML = '<option value="">Carregando...</option>';
            try {
                const url = `${getCorrectUrl('getVendedores')}?action=getVendedores`;
                const response = await fetch(url);
                if (!response.ok) throw new Error('Erro de rede ao buscar vendedores.');
                const data = await response.json();
                if (data.error) throw new Error(data.error);
                selectVendedorForm.innerHTML = '<option value="">Selecione um vendedor</option>';
                const vendedoresUnicos = [...new Set(data)];
                vendedoresUnicos.forEach(nome => {
                    if (nome) {
                        const optionFiltro = document.createElement('option');
                        optionFiltro.value = nome;
                        optionFiltro.textContent = nome;
                        selectVendedorFiltro.appendChild(optionFiltro);
                        const optionForm = document.createElement('option');
                        optionForm.value = nome;
                        optionForm.textContent = nome;
                        selectVendedorForm.appendChild(optionForm);
                    }
                });
            } catch (error) {
                toast(`Erro ao carregar vendedores: ${error.message}`, true);
                selectVendedorForm.innerHTML = '<option value="">Erro ao carregar</option>';
            }
        }

        async function fetchAbastecimentos() {
            try {
                const startDate = document.getElementById('abast-start-date').value;
                const endDate = document.getElementById('abast-end-date').value;
                const listContainer = document.getElementById('list-consultas');
                const summaryContainer = document.getElementById('summary-container');
                if (!startDate || !endDate) { 
                    toast('Selecione data de início e fim.', true); 
                    summaryContainer.innerHTML = '';
                    listContainer.innerHTML = '';
                    return; 
                }
                const url = `${getCorrectUrl('getAbastecimentos')}?action=getAbastecimentos&startDate=${startDate}&endDate=${endDate}`;
                const response = await fetch(url);
                if (!response.ok) throw new Error('Erro de rede.');
                const data = await response.json();
                if (data.error) throw new Error(data.error);
                if (!data || data.length === 0) {
                    summaryContainer.innerHTML = '';
                    listContainer.innerHTML = '<p>Nenhum abastecimento encontrado.</p>';
                    return;
                }
                const totais = data.reduce((acc, item) => {
                    const valorLimpo = String(item.valorpago || '0').replace(/\./g, '').replace(',', '.');
                    const litrosLimpo = String(item.litros || '0').replace(',', '.');
                    acc.totalValor += parseFloat(valorLimpo);
                    acc.totalLitros += parseFloat(litrosLimpo);
                    return acc;
                }, { totalValor: 0, totalLitros: 0 });
                const totalValorFormatado = totais.totalValor.toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' });
                const totalLitrosFormatado = totais.totalLitros.toFixed(2).replace('.', ',') + ' L';
                summaryContainer.innerHTML = `
                    <div class="card summary-card">
                        <div class="card-row">
                            <span class="card-label">Total Gasto (Período):</span>
                            <span>${totalValorFormatado}</span>
                        </div>
                        <div class="card-row">
                            <span class="card-label">Total de Litros:</span>
                            <span>${totalLitrosFormatado}</span>
                        </div>
                    </div>`;
                listContainer.innerHTML = data.map(a => {
                    const dataAbastecimento = new Date(a.data).toLocaleDateString('pt-BR', { timeZone: 'UTC' });
                    const valorPagoLimpo = String(a.valorpago || '0').replace(/\./g, '').replace(',', '.');
                    const valorPorLitroLimpo = String(a.valorporlitro || '0').replace(/\./g, '').replace(',', '.');
                    const valorPago = parseFloat(valorPagoLimpo).toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' });
                    const valorPorLitro = parseFloat(valorPorLitroLimpo).toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' });
                    const abastJson = JSON.stringify(a).replace(/"/g, '&quot;');
                    return `<div class="card">
                                <div class="card-header"><div class="card-title">${a.local}</div><div class="card-date">${dataAbastecimento}</div></div>
                                <div class="card-row"><span class="card-label">Valor Pago:</span><span>${valorPago}</span></div>
                                <div class="card-row"><span class="card-label">Litros:</span><span>${a.litros} L</span></div>
                                <div class="card-row"><span class="card-label">Preço/Litro:</span><span>${valorPorLitro}</span></div>
                                <div class="card-actions">
                                    <button class="btn btn-edit" data-abastecimento='${abastJson}'><i class="fas fa-edit"></i> Editar</button>
                                    <button class="btn btn-delete" data-abastecimento='${abastJson}'><i class="fas fa-trash"></i> Apagar</button>
                                </div>
                            </div>`;
                }).join('');
            } catch (error) {
                document.getElementById('summary-container').innerHTML = '';
                document.getElementById('list-consultas').innerHTML = `<p style="color: red;">Erro: ${error.message}</p>`;
                toast('Erro ao buscar abastecimentos', true);
            }
        }
        
        async function fetchComissoes() {
            try {
                const status = document.getElementById('comissao-status-filter').value;
                const startDate = document.getElementById('comissao-start-date').value;
                const endDate = document.getElementById('comissao-end-date').value;
                const vendedor = document.getElementById('comissao-vendedor-filter').value;
                const listContainer = document.getElementById('list-consultas');
                const summaryContainer = document.getElementById('summary-container');
                if (!startDate || !endDate) { 
                    toast('Selecione o período.', true); 
                    summaryContainer.innerHTML = '';
                    listContainer.innerHTML = '';
                    return; 
                }
                const url = `${getCorrectUrl('getComissoes')}?action=getComissoes&status=${status}&startDate=${startDate}&endDate=${endDate}&vendedor=${encodeURIComponent(vendedor)}`;
                const response = await fetch(url);
                if (!response.ok) throw new Error('Erro de rede.');
                const data = await response.json();
                if (data.error) throw new Error(data.error);
                if (!data || data.length === 0) {
                    summaryContainer.innerHTML = '';
                    listContainer.innerHTML = '<p>Nenhuma comissão encontrada.</p>';
                    return;
                }
                const totalComissao = data.reduce((sum, item) => {
                    const valorStr = String(item.valorcomissao || '0').replace(/\./g, '').replace(',', '.');
                    return sum + parseFloat(valorStr);
                }, 0);
                const totalFormatado = totalComissao.toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' });
                summaryContainer.innerHTML = `<div class="card summary-card"><div class="card-row"><span>Total de Comissões:</span><span>${totalFormatado}</span></div></div>`;
                listContainer.innerHTML = data.map(c => {
                    const dataComissao = new Date(c.data).toLocaleDateString('pt-BR', { timeZone: 'UTC' });
                    const valorStr = String(c.valorcomissao || '0').replace(/\./g, '').replace(',', '.');
                    const valorComissao = parseFloat(valorStr).toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' });
                    const statusClass = c.status.toLowerCase() === 'pago' ? 'badge-pago' : 'badge-pendente';
                    const comissaoJson = JSON.stringify(c).replace(/"/g, '&quot;');
                    return `<div class="card">
                                <div class="card-header"><div class="card-title">${c.cliente}</div><div class="card-date">${dataComissao}</div></div>
                                <div class="card-row"><span class="card-label">Local:</span><span>${c.local}</span></div>
                                <div class="card-row"><span class="card-label">Vendedor:</span><span>${c.vendedor}</span></div>
                                <div class="card-row"><span class="card-label">Valor:</span><span>${valorComissao}</span></div>
                                <div class="card-row"><span class="card-label">Status:</span><span class="badge ${statusClass}">${c.status}</span></div>
                                <div class="card-actions">
                                    <button class="btn btn-edit" data-comissao='${comissaoJson}'><i class="fas fa-edit"></i> Editar</button>
                                    <button class="btn btn-delete" data-comissao='${comissaoJson}'><i class="fas fa-trash"></i> Apagar</button>
                                </div>
                            </div>`;
                }).join('');
            } catch (error) {
                document.getElementById('summary-container').innerHTML = '';
                document.getElementById('list-consultas').innerHTML = `<p style="color: red;">Erro: ${error.message}</p>`;
                toast('Erro ao buscar comissões', true);
            }
        }

        async function fetchPagamentos() {
            try {
                const status = document.getElementById('pagamento-status-filter').value;
                const startDate = document.getElementById('pagamento-start-date').value;
                const endDate = document.getElementById('pagamento-end-date').value;
                const listContainer = document.getElementById('list-consultas');
                if (!startDate || !endDate) { 
                    toast('Selecione o período.', true);
                    listContainer.innerHTML = '';
                    return; 
                }
                const url = `${getCorrectUrl('getPagamentos')}?action=getPagamentos&status=${status}&startDate=${startDate}&endDate=${endDate}`;
                const response = await fetch(url);
                if (!response.ok) throw new Error('Erro de rede');
                const data = await response.json();
                if (data.error) throw new Error(data.error);
                if (!data || data.length === 0) {
                    listContainer.innerHTML = '<p>Nenhum pagamento encontrado.</p>';
                    return;
                }
                listContainer.innerHTML = data.map(p => {
                    const dataPagamento = new Date(p.data).toLocaleDateString('pt-BR', { timeZone: 'UTC' });
                    const valor = parseFloat(p.valor).toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' });
                    const statusClass = p.status.toLowerCase() === 'pago' ? 'badge-pago' : 'badge-pendente';
                    return `<div class="card"><div class="card-header"><div class="card-title">${p.cliente}</div><div class="card-date">${dataPagamento}</div></div><div class="card-row"><span class="card-label">Valor:</span><span>${valor}</span></div><div class="card-row"><span class="card-label">Observação:</span><span>${p.observacao || '-'}</span></div><div class="card-row"><span class="card-label">Status:</span><span class="badge ${statusClass}">${p.status}</span></div></div>`;
                }).join('');
             } catch (error) { 
                document.getElementById('list-consultas').innerHTML = `<p style="color: red;">Erro: ${error.message}</p>`; 
                toast('Erro ao buscar pagamentos', true); 
            }
        }

        document.addEventListener('DOMContentLoaded', () => {
            fetchMotoristas();
            fetchVendedores();
            
            document.getElementById('truck').addEventListener('change', () => {
                if (document.getElementById('sec-consultas').classList.contains('active')) {
                    document.querySelector('.consulta-selector .active').click();
                }
            });

            document.querySelectorAll('.nav-item').forEach(item => {
                item.addEventListener('click', () => {
                    const sec = item.dataset.sec;
                    document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('active'));
                    item.classList.add('active');
                    document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
                    document.getElementById('sec-' + sec).classList.add('active');
                    if (sec === 'consultas') {
                        document.getElementById('btn-select-entregues').click();
                    }
                });
            });

            const consultaSelectors = {
                'btn-select-entregues': { filter: 'filtros-entregues', fetchFn: fetchEntregues },
                'btn-select-abastecimentos': { filter: 'filtros-abastecimentos', fetchFn: fetchAbastecimentos, defaultDates: 7 },
                'btn-select-comissoes': { filter: 'filtros-comissoes', fetchFn: fetchComissoes, defaultDates: 30 },
                'btn-select-pagamentos': { filter: 'filtros-pagamentos', fetchFn: fetchPagamentos, defaultDates: 30 }
            };

            Object.keys(consultaSelectors).forEach(btnId => {
                document.getElementById(btnId).addEventListener('click', (e) => {
                    document.querySelectorAll('.btn-selector').forEach(b => b.classList.remove('active'));
                    document.querySelectorAll('.filter-container').forEach(f => f.style.display = 'none');
                    const selector = consultaSelectors[btnId];
                    e.target.classList.add('active');
                    document.getElementById(selector.filter).style.display = 'block';
                    document.getElementById('summary-container').innerHTML = '';
                    document.getElementById('list-consultas').innerHTML = '<p>Buscando...</p>';
                    if (selector.defaultDates) {
                        const startInputId = btnId.replace('btn-select-', '') + '-start-date';
                        const endInputId = btnId.replace('btn-select-', '') + '-end-date';
                        if (!document.getElementById(startInputId).value || !document.getElementById(endInputId).value) {
                            const hoje = new Date(); const diasAtras = new Date();
                            diasAtras.setDate(hoje.getDate() - selector.defaultDates);
                            document.getElementById(endInputId).value = hoje.toISOString().split('T')[0];
                            document.getElementById(startInputId).value = diasAtras.toISOString().split('T')[0];
                        }
                    }
                    selector.fetchFn();
                });
            });
            
            async function handleSearch(btnId, fetchFn) {
                const btn = document.getElementById(btnId);
                const originalBtnHTML = btn.innerHTML;
                btn.innerHTML = '<div class="spinner"></div>';
                btn.disabled = true;
                document.getElementById('summary-container').innerHTML = '';
                document.getElementById('list-consultas').innerHTML = '<p>Buscando...</p>';
                try {
                    await fetchFn();
                } finally {
                    btn.innerHTML = originalBtnHTML;
                    btn.disabled = false;
                }
            }

            document.getElementById('btn-fetch-entregues').addEventListener('click', () => handleSearch('btn-fetch-entregues', fetchEntregues));
            document.getElementById('btn-fetch-abastecimentos').addEventListener('click', () => handleSearch('btn-fetch-abastecimentos', fetchAbastecimentos));
            document.getElementById('btn-fetch-comissoes').addEventListener('click', () => handleSearch('btn-fetch-comissoes', fetchComissoes));
            document.getElementById('btn-fetch-pagamentos').addEventListener('click', () => handleSearch('btn-fetch-pagamentos', fetchPagamentos));
            
            document.getElementById('btn-cancelar-edicao-venda').addEventListener('click', resetVendaForm);
            document.getElementById('btn-cancelar-edicao-abast').addEventListener('click', resetAbastecimentoForm);
            document.getElementById('btn-cancelar-edicao-comissao').addEventListener('click', resetComissaoForm);
            
            document.getElementById('list-consultas').addEventListener('click', (e) => {
                const editButton = e.target.closest('.btn-edit');
                if (editButton) {
                    if (editButton.dataset.venda) handleEditVendaClick(JSON.parse(editButton.dataset.venda));
                    if (editButton.dataset.abastecimento) handleEditAbastecimentoClick(JSON.parse(editButton.dataset.abastecimento));
                    if (editButton.dataset.comissao) handleEditComissaoClick(JSON.parse(editButton.dataset.comissao));
                }
                const deleteButton = e.target.closest('.btn-delete');
                if (deleteButton) {
                    if (deleteButton.disabled) return;
                    if (deleteButton.dataset.venda) handleDeleteVendaClick(JSON.parse(deleteButton.dataset.venda), deleteButton);
                    if (deleteButton.dataset.abastecimento) handleDeleteAbastecimentoClick(JSON.parse(deleteButton.dataset.abastecimento), deleteButton);
                    if (deleteButton.dataset.comissao) handleDeleteComissaoClick(JSON.parse(deleteButton.dataset.comissao), deleteButton);
                }
            });

            document.getElementById('form-vendas').addEventListener('submit', async (e) => {
                e.preventDefault();
                const btn = document.getElementById('btn-gravar-venda');
                const originalBtnHTML = btn.innerHTML;
                btn.innerHTML = '<div class="spinner"></div>';
                btn.disabled = true;
                const rowNumber = document.getElementById('v-row-number').value;
                const isEditing = !!rowNumber;
                const payload = { 
                    type: isEditing ? 'editVenda' : 'venda',
                    dataVenda: document.getElementById('v-data').value, 
                    cidade: document.getElementById('v-cidade').value, 
                    cliente: document.getElementById('v-cliente').value, 
                    valorVendido: parseFloat(document.getElementById('v-valor').value),
                    dataCadastro: isEditing ? document.getElementById('v-data-cadastro').value : getNow(),
                    material: document.getElementById('v-material').value, 
                    valorDieselGasto: parseFloat(document.getElementById('v-diesel').value || 0), 
                    valorParaEncher: parseFloat(document.getElementById('v-carga').value || 0), 
                    gastoAleatorio: parseFloat(document.getElementById('v-extra').value || 0), 
                    despesasAleatorias: document.getElementById('v-desc').value,
                    motorista: document.getElementById('v-motorista').value,
                    comissaoValor: parseFloat(document.getElementById('v-comissao').value || 0),
                    statusVenda: document.getElementById('v-status-venda').value
                };
                if (isEditing) { payload.rowNumber = parseInt(rowNumber, 10); }
                try {
                    await fetch(getCorrectUrl(payload.type), { method: 'POST', mode: 'no-cors', body: JSON.stringify(payload) }); 
                    toast(isEditing ? 'Alterações salvas!' : 'Venda registrada!'); 
                    resetVendaForm();
                    if (isEditing) {
                        document.querySelector('.nav-item[data-sec="consultas"]').click();
                    }
                } catch (err) { 
                    toast('Erro ao registrar', true); 
                } finally {
                    btn.innerHTML = originalBtnHTML;
                    btn.disabled = false;
                }
            });

            document.getElementById('form-abastecimento').addEventListener('submit', async (e) => {
                e.preventDefault();
                const btn = document.getElementById('btn-gravar-abast');
                const originalBtnHTML = btn.innerHTML;
                btn.innerHTML = '<div class="spinner"></div>';
                btn.disabled = true;
                const rowNumber = document.getElementById('a-row-number').value;
                const isEditing = !!rowNumber;
                const payload = {
                    type: isEditing ? 'editAbastecimento' : 'abastecimento',
                    data: document.getElementById('a-data').value,
                    dataCadastro: isEditing ? document.getElementById('a-data-cadastro').value : getNow(),
                    local: document.getElementById('a-local').value,
                    valorPago: parseFloat(document.getElementById('a-valor').value),
                    litros: parseFloat(document.getElementById('a-litros').value),
                    valorPorLitro: parseFloat(document.getElementById('a-preco').value)
                };
                if (isEditing) payload.rowNumber = parseInt(rowNumber, 10);
                try {
                    await fetch(getCorrectUrl(payload.type), { method: 'POST', mode: 'no-cors', body: JSON.stringify(payload) });
                    toast(isEditing ? 'Alterações salvas!' : 'Abastecimento registrado!');
                    resetAbastecimentoForm();
                    if (isEditing) {
                        document.querySelector('.nav-item[data-sec="consultas"]').click();
                        document.getElementById('btn-select-abastecimentos').click();
                    }
                } catch (err) { 
                    toast('Erro ao registrar', true); 
                } finally {
                    btn.innerHTML = originalBtnHTML;
                    btn.disabled = false;
                }
            });

            document.getElementById('form-comissao').addEventListener('submit', async (e) => {
                e.preventDefault();
                const btn = document.getElementById('btn-gravar-comissao');
                const originalBtnHTML = btn.innerHTML;
                btn.innerHTML = '<div class="spinner"></div>';
                btn.disabled = true;
                const rowNumber = document.getElementById('c-row-number').value;
                const isEditing = !!rowNumber;
                const payload = {
                    type: isEditing ? 'editComissao' : 'comissao',
                    data: document.getElementById('c-data').value,
                    dataCadastro: isEditing ? document.getElementById('c-data-cadastro').value : getNow(),
                    cliente: document.getElementById('c-cliente').value,
                    local: document.getElementById('c-local').value,
                    material: document.getElementById('c-material').value,
                    valorComissao: parseFloat(document.getElementById('c-valor').value),
                    vendedor: document.getElementById('c-vendedor').value,
                    status: document.getElementById('c-status').value
                };
                if (isEditing) payload.rowNumber = parseInt(rowNumber, 10);
                try {
                    await fetch(getCorrectUrl(payload.type), { mode: 'no-cors', method: 'POST', body: JSON.stringify(payload) });
                    toast(isEditing ? 'Alterações salvas!' : 'Comissão registrada!');
                    resetComissaoForm();
                    if (isEditing) {
                        document.querySelector('.nav-item[data-sec="consultas"]').click();
                        document.getElementById('btn-select-comissoes').click();
                    }
                } catch (err) { 
                    toast('Erro ao registrar', true); 
                } finally {
                    btn.innerHTML = originalBtnHTML;
                    btn.disabled = false;
                }
            });
            
            document.getElementById('form-pagamento').addEventListener('submit', async (e) => { 
                e.preventDefault(); 
                const btn = document.getElementById('btn-registrar-pagamento');
                const originalBtnHTML = btn.innerHTML;
                btn.innerHTML = '<div class="spinner"></div>';
                btn.disabled = true;
                try { 
                    const payload = { 
                        type: 'pagamento', 
                        data: document.getElementById('p-data').value, 
                        cliente: document.getElementById('p-cliente').value, 
                        valor: parseFloat(document.getElementById('p-valor').value), 
                        status: document.getElementById('p-status').value, 
                        observacao: document.getElementById('p-obs').value, 
                        dataCadastro: getNow() 
                    };
                    await fetch(getCorrectUrl('pagamento'), { method: 'POST', mode: 'no-cors', body: JSON.stringify(payload) }); 
                    toast('Pagamento registrado!'); 
                    e.target.reset(); 
                } catch (err) { 
                    toast('Erro ao registrar', true); 
                } finally {
                    btn.innerHTML = originalBtnHTML;
                    btn.disabled = false;
                }
            });
        });
    </script>
</body>
</html>
