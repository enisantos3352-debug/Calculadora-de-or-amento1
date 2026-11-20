
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Calculadora de Orçamento de Reparo</title>
  <style>
    :root {
      --bg: #f3f6fa;
      --card: #ffffff;
      --text: #16202a;
      --muted: #5c6b7a;
      --primary: #0f766e;
      --primary-dark: #115e59;
      --whatsapp: #16a34a;
      --whatsapp-dark: #15803d;
      --accent: #2563eb;
      --border: #dce3ec;
      --soft: #eef6f5;
    }

    * {
      box-sizing: border-box;
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
    }

    body {
      margin: 0;
      padding: 16px;
      background: var(--bg);
      color: var(--text);
    }

    .container {
      max-width: 780px;
      margin: 0 auto;
      display: grid;
      gap: 16px;
    }

    .card {
      background: var(--card);
      border: 1px solid var(--border);
      border-radius: 14px;
      padding: 18px;
      box-shadow: 0 4px 14px rgba(15, 23, 42, 0.05);
    }

    h1 {
      margin: 0 0 6px;
      font-size: 1.35rem;
    }

    h2 {
      margin: 0 0 12px;
      font-size: 1.05rem;
    }

    p.sub {
      margin: 0;
      color: var(--muted);
      font-size: 0.92rem;
    }

    .grid-2 {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
      gap: 12px;
    }

    .field {
      display: flex;
      flex-direction: column;
      gap: 5px;
    }

    label {
      font-size: 0.86rem;
      font-weight: 600;
      color: var(--text);
    }

    input, select, textarea {
      width: 100%;
      padding: 10px 12px;
      border: 1px solid #cbd5e1;
      border-radius: 10px;
      font-size: 0.96rem;
      color: var(--text);
      background: #fff;
    }

    input:focus, select:focus, textarea:focus {
      outline: 2px solid rgba(15, 118, 110, 0.25);
      border-color: var(--primary);
    }

    .summary {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(170px, 1fr));
      gap: 10px;
      margin-top: 8px;
    }

    .box {
      background: var(--soft);
      border: 1px solid #cce7e3;
      border-radius: 12px;
      padding: 12px;
    }

    .box .k {
      font-size: 0.8rem;
      color: var(--muted);
    }

    .box .v {
      font-size: 1.2rem;
      font-weight: 700;
      margin-top: 4px;
      color: var(--primary-dark);
    }

    .bar-wrap {
      margin-top: 14px;
    }

    .bar {
      display: flex;
      height: 16px;
      border-radius: 999px;
      overflow: hidden;
      background: #e2e8f0;
    }

    .bar-pecas { background: #0f766e; }
    .bar-mao { background: #2563eb; }
    .bar-lucro { background: #d97706; }

    .legend {
      display: flex;
      flex-wrap: wrap;
      gap: 14px;
      margin-top: 8px;
      font-size: 0.82rem;
      color: var(--muted);
    }

    .dot {
      display: inline-block;
      width: 10px;
      height: 10px;
      border-radius: 50%;
      margin-right: 5px;
    }

    textarea {
      min-height: 170px;
      resize: vertical;
      line-height: 1.45;
    }

    .actions {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      margin-top: 12px;
    }

    button {
      border: none;
      border-radius: 10px;
      padding: 11px 14px;
      font-size: 0.92rem;
      font-weight: 600;
      cursor: pointer;
      color: #fff;
    }

    .btn-primary { background: var(--primary); }
    .btn-primary:hover { background: var(--primary-dark); }

    .btn-wa { background: var(--whatsapp); }
    .btn-wa:hover { background: var(--whatsapp-dark); }

    .btn-blue { background: var(--accent); }

    .btn-secondary {
      background: #475569;
    }

    .link-box {
      margin-top: 12px;
      padding: 12px;
      border-radius: 10px;
      background: #f8fafc;
      border: 1px dashed #94a3b8;
      word-break: break-all;
      font-size: 0.85rem;
    }

    .cliente-view {
      display: none;
    }

    .faq-btns {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
      margin: 12px 0;
    }

    .faq-btn {
      background: #f1f5f9;
      color: #0f172a;
      border: 1px solid #cbd5e1;
      font-size: 0.84rem;
      padding: 8px 11px;
    }

    .status-msg {
      margin-top: 8px;
      font-size: 0.86rem;
      color: var(--primary-dark);
      font-weight: 600;
      min-height: 20px;
    }
  </style>
</head>
<body>
  <div class="container">
    <!-- TELA DO TÉCNICO -->
    <div id="tecnicoView">
      <div class="card">
        <h1>Calculadora de Orçamento de Reparo</h1>
        <p class="sub">Calcule peças, mão de obra, deslocamento e gere o orçamento com link de aprovação do cliente.</p>
      </div>

      <div class="card">
        <h2>1. Valores e Serviço</h2>
        <div class="grid-2">
          <div class="field">
            <label for="equipamento">Equipamento / Serviço</label>
            <input id="equipamento" type="text" value="Placa / Lavadora" />
          </div>
          <div class="field">
            <label for="cliente">Nome do Cliente</label>
            <input id="cliente" type="text" placeholder="Ex.: Maria" />
          </div>
          <div class="field">
            <label for="pecas">Custo das Peças (R$)</label>
            <input id="pecas" type="number" step="0.01" min="0" value="65" />
          </div>
          <div class="field">
            <label for="horas">Tempo de Serviço (horas)</label>
            <input id="horas" type="number" step="0.5" min="0" value="2" />
          </div>
          <div class="field">
            <label for="valorHora">Valor da Hora / Bancada (R$)</label>
            <input id="valorHora" type="number" step="0.01" min="0" value="50" />
          </div>
          <div class="field">
            <label for="deslocamento">Deslocamento / Taxa Extra (R$)</label>
            <input id="deslocamento" type="number" step="0.01" min="0" value="20" />
          </div>
          <div class="field">
            <label for="margem">Margem de Lucro (%)</label>
            <input id="margem" type="number" step="1" min="0" value="25" />
          </div>
          <div class="field">
            <label for="prazo">Prazo Estimado</label>
            <input id="prazo" type="text" value="1 a 2 dias úteis" />
          </div>
          <div class="field">
            <label for="garantia">Garantia do Serviço</label>
            <input id="garantia" type="text" value="90 dias" />
          </div>
          <div class="field">
            <label for="pagamento">Formas de Pagamento</label>
            <input id="pagamento" type="text" value="Pix ou Cartão" />
          </div>
          <div class="field">
            <label for="whatsTecnico">Seu WhatsApp (com DDD)</label>
            <input id="whatsTecnico" type="text" placeholder="Ex.: 85999999999" />
          </div>
        </div>

        <div class="summary">
          <div class="box">
            <div class="k">Custo Base</div>
            <div class="v" id="outCusto">R$ 0,00</div>
          </div>
          <div class="box">
            <div class="k">Lucro Estimado</div>
            <div class="v" id="outLucro">R$ 0,00</div>
          </div>
          <div class="box">
            <div class="k">Total do Orçamento</div>
            <div class="v" id="outTotal">R$ 0,00</div>
          </div>
        </div>

        <div class="bar-wrap">
          <div class="bar">
            <div id="barPecas" class="bar-pecas" style="width: 33%"></div>
            <div id="barMao" class="bar-mao" style="width: 34%"></div>
            <div id="barLucro" class="bar-lucro" style="width: 33%"></div>
          </div>
          <div class="legend">
            <span><i class="dot" style="background:#0f766e"></i>Peças: <strong id="legPecas">0%</strong></span>
            <span><i class="dot" style="background:#2563eb"></i>Mão de obra + desloc.: <strong id="legMao">0%</strong></span>
            <span><i class="dot" style="background:#d97706"></i>Margem/Lucro: <strong id="legLucro">0%</strong></span>
          </div>
        </div>
      </div>

      <div class="card">
        <h2>2. Mensagem Pronta e Aprovação do Cliente</h2>
        <textarea id="textoOrcamento"></textarea>

        <div class="link-box">
          <strong>Link de Aprovação do Cliente:</strong>
          <div id="linkAprovacao">Gerando link...</div>
        </div>

        <div class="actions">
          <button class="btn-primary" type="button" onclick="copiarTexto()">Copiar Orçamento</button>
          <button class="btn-wa" type="button" onclick="enviarWhatsApp()">Enviar no WhatsApp</button>
          <button class="btn-blue" type="button" onclick="gerarLinkAprovacao()">Atualizar Link de Aprovação</button>
          <button class="btn-secondary" type="button" onclick="abrirTelaCliente()">Ver Como o Cliente Vê</button>
        </div>
        <div id="statusMsg" class="status-msg"></div>
      </div>
    </div>

    <!-- TELA DO CLIENTE PARA APROVAR OU TIRAR DÚVIDAS -->
    <div id="clienteView" class="card cliente-view">
      <h2>Aprovação de Orçamento</h2>
      <p class="sub">Confira os detalhes abaixo e escolha uma opção para responder no WhatsApp:</p>
      <div id="resumoCliente" class="link-box" style="white-space: pre-line; background:#fff;"></div>

      <p class="sub" style="margin-top:12px;"><strong>Dúvidas rápidas (clique para montar a pergunta):</strong></p>
      <div class="faq-btns">
        <button class="faq-btn" type="button" onclick="perguntarCliente('Tenho dúvida sobre o prazo de entrega desse serviço.')">Qual o prazo exato?</button>
        <button class="faq-btn" type="button" onclick="perguntarCliente('Como funciona a garantia desse reparo?')">Como é a garantia?</button>
        <button class="faq-btn" type="button" onclick="perguntarCliente('Pode me passar a chave Pix ou condições de pagamento?')">Formas de pagamento</button>
      </div>

      <div class="actions">
        <button class="btn-wa" type="button" onclick="aprovarOrcamento()">APROVAR ORÇAMENTO</button>
        <button class="btn-blue" type="button" onclick="tirarDuvida()">TIRAR DÚVIDA NO WHATSAPP</button>
        <button class="btn-secondary" type="button" onclick="voltarTecnico()">Voltar para Calculadora</button>
      </div>
    </div>
  </div>

  <script>
    const ids = [
      "equipamento", "cliente", "pecas", "horas", "valorHora",
      "deslocamento", "margem", "prazo", "garantia", "pagamento", "whatsTecnico"
    ];

    function fmt(v) {
      return Number(v || 0).toLocaleString("pt-BR", { style: "currency", currency: "BRL" });
    }

    function limparFone(fone) {
      let digitos = (fone || "").replace(/\D/g, "");
      if (digitos && !digitos.startsWith("55") && (digitos.length === 10 || digitos.length === 11)) {
        digitos = "55" + digitos;
      }
      return digitos;
    }

    function obterDados() {
      const pecas = Math.max(0, parseFloat(document.getElementById("pecas").value) || 0);
      const horas = Math.max(0, parseFloat(document.getElementById("horas").value) || 0);
      const valorHora = Math.max(0, parseFloat(document.getElementById("valorHora").value) || 0);
      const deslocamento = Math.max(0, parseFloat(document.getElementById("deslocamento").value) || 0);
      const margem = Math.max(0, parseFloat(document.getElementById("margem").value) || 0);

      const maoObraTotal = (horas * valorHora) + deslocamento;
      const custoBase = pecas + maoObraTotal;
      const lucro = custoBase * (margem / 100);
      const total = custoBase + lucro;

      return {
        equipamento: document.getElementById("equipamento").value.trim() || "Serviço de Reparo",
        cliente: document.getElementById("cliente").value.trim() || "Cliente",
        pecas, maoObraTotal, custoBase, lucro, total,
        prazo: document.getElementById("prazo").value.trim() || "A combinar",
        garantia: document.getElementById("garantia").value.trim() || "90 dias",
        pagamento: document.getElementById("pagamento").value.trim() || "Pix ou dinheiro",
        whatsTecnico: document.getElementById("whatsTecnico").value.trim()
      };
    }

    function buildLink(d) {
      const params = new URLSearchParams({
        aprovar: "1",
        c: d.cliente,
        e: d.equipamento,
        t: d.total.toFixed(2),
        p: d.prazo,
        g: d.garantia,
        pg: d.pagamento,
        w: limparFone(d.whatsTecnico)
      });
      const base = window.location.href.split("?")[0];
      return `${base}?${params.toString()}`;
    }

    function calcular() {
      const d = obterDados();
      document.getElementById("outCusto").textContent = fmt(d.custoBase);
      document.getElementById("outLucro").textContent = fmt(d.lucro);
      document.getElementById("outTotal").textContent = fmt(d.total);

      const baseBarra = d.total > 0 ? d.total : 1;
      const pPecas = (d.pecas / baseBarra) * 100;
      const pMao = (d.maoObraTotal / baseBarra) * 100;
      const pLucro = Math.max(0, 100 - pPecas - pMao);

      document.getElementById("barPecas").style.width = `${pPecas}%`;
      document.getElementById("barMao").style.width = `${pMao}%`;
      document.getElementById("barLucro").style.width = `${pLucro}%`;

      document.getElementById("legPecas").textContent = `${pPecas.toFixed(0)}%`;
      document.getElementById("legMao").textContent = `${pMao.toFixed(0)}%`;
      document.getElementById("legLucro").textContent = `${pLucro.toFixed(0)}%`;

      const link = buildLink(d);
      document.getElementById("linkAprovacao").textContent = link;

      const msg = [
        `Olá, ${d.cliente}! Segue o orçamento para *${d.equipamento}*:`,
        ``,
        `• Valor total: *${fmt(d.total)}*`,
        `• Prazo estimado: ${d.prazo}`,
        `• Garantia: ${d.garantia}`,
        `• Pagamento: ${d.pagamento}`,
        ``,
        `Para aprovar ou tirar dúvida rápido, acesse:`,
        `${link}`
      ].join("\n");

      document.getElementById("textoOrcamento").value = msg;
    }

    function setStatus(txt) {
      document.getElementById("statusMsg").textContent = txt;
    }

    function copiarTexto() {
      const ta = document.getElementById("textoOrcamento");
      ta.select();
      navigator.clipboard?.writeText(ta.value);
      setStatus("Orçamento copiado! Agora é só colar no WhatsApp.");
    }

    function abrirUrlWhats(fone, texto) {
      const url = fone
        ? `https://wa.me/${fone}?text=${encodeURIComponent(texto)}`
        : `https://wa.me/?text=${encodeURIComponent(texto)}`;
      window.open(url, "_blank");
    }

    function enviarWhatsApp() {
      const d = obterDados();
      abrirUrlWhats("", document.getElementById("textoOrcamento").value);
      setStatus("Abrindo WhatsApp com o orçamento pronto.");
    }

    function gerarLinkAprovacao() {
      calcular();
      const link = document.getElementById("linkAprovacao").textContent;
      navigator.clipboard?.writeText(link);
      setStatus("Link de aprovação atualizado e copiado!");
    }

    let dadosAtuaisCliente = null;
    let perguntaSelecionada = "";

    function montarTelaCliente(dados) {
      dadosAtuaisCliente = dados;
      perguntaSelecionada = "";
      document.getElementById("resumoCliente").textContent = [
        `Cliente: ${dados.cliente}`,
        `Serviço/Item: ${dados.equipamento}`,
        `Valor Total: ${fmt(dados.total)}`,
        `Prazo: ${dados.prazo}`,
        `Garantia: ${dados.garantia}`,
        `Pagamento: ${dados.pagamento}`
      ].join("\n");

      document.getElementById("tecnicoView").style.display = "none";
      document.getElementById("clienteView").style.display = "block";
    }

    function abrirTelaCliente() {
      const d = obterDados();
      montarTelaCliente({
        cliente: d.cliente,
        equipamento: d.equipamento,
        total: d.total,
        prazo: d.prazo,
        garantia: d.garantia,
        pagamento: d.pagamento,
        whatsTecnico: limparFone(d.whatsTecnico)
      });
    }

    function voltarTecnico() {
      document.getElementById("clienteView").style.display = "none";
      document.getElementById("tecnicoView").style.display = "block";
    }

    function perguntarCliente(texto) {
      perguntaSelecionada = texto;
      tirarDuvida();
    }

    function aprovarOrcamento() {
      const c = dadosAtuaisCliente || obterDados();
      const msg = `Olá! APROVO o orçamento de *${c.equipamento}* no valor de *${fmt(c.total)}* (Prazo: ${c.prazo} | Garantia: ${c.garantia}). Cliente: ${c.cliente}.`;
      abrirUrlWhats(c.whatsTecnico || "", msg);
    }

    function tirarDuvida() {
      const c = dadosAtuaisCliente || obterDados();
      const detalhe = perguntaSelecionada || `Tenho uma dúvida sobre o orçamento de *${c.equipamento}* (${fmt(c.total)}).`;
      const msg = `Olá! Sou ${c.cliente}. ${detalhe}`;
      abrirUrlWhats(c.whatsTecnico || "", msg);
    }

    ids.forEach(id => {
      document.getElementById(id).addEventListener("input", calcular);
    });

    // Verifica se o link foi aberto no modo de aprovação do cliente
    const qs = new URLSearchParams(window.location.search);
    if (qs.get("aprovar") === "1") {
      montarTelaCliente({
        cliente: qs.get("c") || "Cliente",
        equipamento: qs.get("e") || "Serviço de Reparo",
        total: parseFloat(qs.get("t") || "0") || 0,
        prazo: qs.get("p") || "A combinar",
        garantia: qs.get("g") || "90 dias",
        pagamento: qs.get("pg") || "Pix ou dinheiro",
        whatsTecnico: qs.get("w") || ""
      });
    } else {
      calcular();
    }
  </script>
</body>
</html>
