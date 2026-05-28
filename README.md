
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Diagnóstico Personalizado — Pulso Financeiro</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --green: #2ECC71;
    --green-dim: #1a7a43;
    --black: #080808;
    --surface: #111111;
    --surface2: #1a1a1a;
    --border: rgba(255,255,255,0.08);
    --text: #ffffff;
    --muted: rgba(255,255,255,0.45);
  }

  html { scroll-behavior: smooth; }

  body {
    background: var(--black);
    color: var(--text);
    font-family: 'DM Sans', sans-serif;
    min-height: 100vh;
    overflow-x: hidden;
  }

  .pulse-bg {
    position: fixed;
    top: 0; left: 0; right: 0;
    height: 3px;
    background: var(--green);
    z-index: 100;
  }

  .hero {
    padding: 80px 24px 60px;
    max-width: 560px;
    margin: 0 auto;
    text-align: center;
  }

  .logo-wrap {
    display: inline-flex;
    align-items: center;
    gap: 12px;
    margin-bottom: 48px;
  }

  .logo-svg { width: 44px; height: 30px; }

  .logo-name {
    font-family: 'Syne', sans-serif;
    font-weight: 800;
    font-size: 18px;
    letter-spacing: 0.12em;
    color: var(--text);
  }

  .hero-tag {
    display: inline-block;
    font-size: 11px;
    font-weight: 500;
    letter-spacing: 0.14em;
    text-transform: uppercase;
    color: var(--green);
    border: 1px solid var(--green);
    padding: 6px 16px;
    border-radius: 100px;
    margin-bottom: 28px;
  }

  .hero h1 {
    font-family: 'Syne', sans-serif;
    font-size: clamp(36px, 8vw, 56px);
    font-weight: 800;
    line-height: 1.05;
    margin-bottom: 20px;
    letter-spacing: -0.02em;
  }

  .hero h1 span { color: var(--green); }

  .hero p {
    font-size: 17px;
    color: var(--muted);
    line-height: 1.7;
    max-width: 420px;
    margin: 0 auto 48px;
  }

  .pulse-line {
    width: 100%;
    max-width: 320px;
    margin: 0 auto 60px;
    display: block;
  }

  .form-wrap {
    max-width: 520px;
    margin: 0 auto;
    padding: 0 24px 80px;
  }

  .field {
    margin-bottom: 20px;
    opacity: 0;
    transform: translateY(20px);
    animation: fadeUp 0.5s forwards;
  }

  .field:nth-child(1) { animation-delay: 0.1s; }
  .field:nth-child(2) { animation-delay: 0.18s; }
  .field:nth-child(3) { animation-delay: 0.26s; }
  .field:nth-child(4) { animation-delay: 0.34s; }
  .field:nth-child(5) { animation-delay: 0.42s; }
  .field:nth-child(6) { animation-delay: 0.50s; }
  .field:nth-child(7) { animation-delay: 0.58s; }

  @keyframes fadeUp {
    to { opacity: 1; transform: translateY(0); }
  }

  label {
    display: block;
    font-size: 12px;
    font-weight: 500;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    color: var(--muted);
    margin-bottom: 8px;
  }

  input, select, textarea {
    width: 100%;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 16px 18px;
    font-family: 'DM Sans', sans-serif;
    font-size: 16px;
    color: var(--text);
    outline: none;
    transition: border-color 0.2s, background 0.2s;
    -webkit-appearance: none;
  }

  input::placeholder, textarea::placeholder { color: rgba(255,255,255,0.2); }

  select { cursor: pointer; }
  select option { background: #1a1a1a; }

  input:focus, select:focus, textarea:focus {
    border-color: var(--green);
    background: var(--surface2);
  }

  textarea { resize: none; min-height: 100px; line-height: 1.6; }

  .radio-group {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
  }

  .radio-opt {
    display: flex;
    align-items: center;
    gap: 10px;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 14px 16px;
    cursor: pointer;
    transition: border-color 0.2s, background 0.2s;
    font-size: 14px;
    color: rgba(255,255,255,0.7);
  }

  .radio-opt:hover { border-color: rgba(46,204,113,0.4); }

  .radio-opt input[type="radio"] { display: none; }

  .radio-opt.selected {
    border-color: var(--green);
    background: rgba(46,204,113,0.08);
    color: var(--text);
  }

  .radio-dot {
    width: 16px; height: 16px;
    border-radius: 50%;
    border: 2px solid rgba(255,255,255,0.2);
    flex-shrink: 0;
    transition: all 0.2s;
    display: flex; align-items: center; justify-content: center;
  }

  .radio-opt.selected .radio-dot {
    border-color: var(--green);
    background: var(--green);
  }

  .radio-opt.selected .radio-dot::after {
    content: '';
    width: 6px; height: 6px;
    border-radius: 50%;
    background: var(--black);
  }

  .divider {
    height: 1px;
    background: var(--border);
    margin: 32px 0;
  }

  .submit-btn {
    width: 100%;
    background: var(--green);
    color: var(--black);
    border: none;
    border-radius: 12px;
    padding: 20px;
    font-family: 'Syne', sans-serif;
    font-size: 16px;
    font-weight: 700;
    letter-spacing: 0.04em;
    cursor: pointer;
    transition: background 0.2s, transform 0.1s;
    margin-top: 8px;
  }

  .submit-btn:hover { background: #27ae60; }
  .submit-btn:active { transform: scale(0.99); }

  .footer-note {
    text-align: center;
    margin-top: 20px;
    font-size: 13px;
    color: var(--muted);
    line-height: 1.6;
  }

  .success-screen {
    display: none;
    text-align: center;
    padding: 80px 24px;
    max-width: 480px;
    margin: 0 auto;
  }

  .success-screen.active { display: block; }

  .success-icon {
    width: 64px; height: 64px;
    border-radius: 50%;
    background: rgba(46,204,113,0.1);
    border: 2px solid var(--green);
    display: flex; align-items: center; justify-content: center;
    margin: 0 auto 32px;
    font-size: 28px;
  }

  .success-screen h2 {
    font-family: 'Syne', sans-serif;
    font-size: 32px;
    font-weight: 800;
    margin-bottom: 16px;
  }

  .success-screen p {
    font-size: 16px;
    color: var(--muted);
    line-height: 1.7;
  }

  .section-title {
    font-family: 'Syne', sans-serif;
    font-size: 13px;
    font-weight: 700;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--green);
    margin-bottom: 20px;
  }
</style>
</head>
<body>

<div class="pulse-bg"></div>

<div class="hero">
  <div class="logo-wrap">
    <svg class="logo-svg" viewBox="0 0 88 30" fill="none" xmlns="http://www.w3.org/2000/svg">
      <polyline points="0,15 14,15 21,3 28,24 34,8 40,18 46,15 88,15" stroke="#2ECC71" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"/>
    </svg>
    <span class="logo-name">PULSO</span>
  </div>

  <div class="hero-tag">Diagnóstico Personalizado</div>

  <h1>Sua empresa tem<br><span>pulso financeiro?</span></h1>

  <p>Preencha as informações abaixo. Em até 24h entramos em contato para agendar sua análise — 30 minutos que vão mostrar exatamente onde o dinheiro da sua empresa está indo.</p>
</div>

<div class="form-wrap">
  <form id="diagForm">

    <p class="section-title">Sobre você</p>

    <div class="field">
      <label>Seu nome</label>
      <input type="text" placeholder="Como podemos te chamar?" required>
    </div>

    <div class="field">
      <label>WhatsApp</label>
      <input type="tel" placeholder="(00) 00000-0000" required>
    </div>

    <div class="field">
      <label>Nome da empresa</label>
      <input type="text" placeholder="Qual o nome do seu negócio?" required>
    </div>

    <div class="field">
      <label>Segmento</label>
      <select required>
        <option value="" disabled selected>Qual é o seu segmento?</option>
        <option>Oficina / Mecânica</option>
        <option>Comércio / Loja física</option>
        <option>Restaurante / Alimentação</option>
        <option>Clínica / Saúde</option>
        <option>Prestador de serviços</option>
        <option>Indústria / Fabricação</option>
        <option>Outro</option>
      </select>
    </div>

    <div class="divider"></div>
    <p class="section-title">Sobre o negócio</p>

    <div class="field">
      <label>Faturamento mensal</label>
      <div class="radio-group">
        <label class="radio-opt" onclick="selectRadio(this)">
          <input type="radio" name="fat" value="30-60k">
          <div class="radio-dot"></div>
          R$30k – R$60k
        </label>
        <label class="radio-opt" onclick="selectRadio(this)">
          <input type="radio" name="fat" value="60-100k">
          <div class="radio-dot"></div>
          R$60k – R$100k
        </label>
        <label class="radio-opt" onclick="selectRadio(this)">
          <input type="radio" name="fat" value="100-200k">
          <div class="radio-dot"></div>
          R$100k – R$200k
        </label>
        <label class="radio-opt" onclick="selectRadio(this)">
          <input type="radio" name="fat" value="200k+">
          <div class="radio-dot"></div>
          Acima de R$200k
        </label>
      </div>
    </div>

    <div class="field">
      <label>Maior dor financeira hoje</label>
      <select required>
        <option value="" disabled selected>O que mais te preocupa?</option>
        <option>Não saber quanto sobra no fim do mês</option>
        <option>Faturar mas não ter caixa</option>
        <option>Não saber se estou comprando certo</option>
        <option>Não entender minha margem de lucro</option>
        <option>Crescer mas sentir que está regredindo</option>
        <option>Não ter controle do fluxo de caixa</option>
        <option>Outro</option>
      </select>
    </div>

    <div class="field">
      <label>Algo que queira compartilhar antes da reunião? <span style="opacity:0.4">(opcional)</span></label>
      <textarea placeholder="Pode contar um pouco sobre a situação atual do seu negócio..."></textarea>
    </div>

    <button type="submit" class="submit-btn">Quero meu diagnóstico personalizado →</button>

    <p class="footer-note">Entraremos em contato pelo WhatsApp em até 24h.<br>Sem compromisso. Sem enrolação.</p>

  </form>

  <div class="success-screen" id="successScreen">
    <div class="success-icon">✓</div>
    <h2>Diagnóstico<br><span style="color:var(--green)">solicitado!</span></h2>
    <p style="margin-top:16px">Recebemos suas informações.<br>Entraremos em contato pelo WhatsApp em até 24h para agendar sua análise.</p>
    <p style="margin-top:24px;font-size:14px;opacity:0.4">@pulsocfo</p>
  </div>
</div>

<script>
function selectRadio(el) {
  document.querySelectorAll('.radio-opt').forEach(r => r.classList.remove('selected'));
  el.classList.add('selected');
}

document.getElementById('diagForm').addEventListener('submit', function(e) {
  e.preventDefault();
  this.style.display = 'none';
  document.getElementById('successScreen').classList.add('active');
  window.scrollTo({ top: 0, behavior: 'smooth' });
});
</script>
</body>
</html>
