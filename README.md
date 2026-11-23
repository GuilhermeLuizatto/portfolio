# Portfólio — Guilherme Luizatto

Desenvolvimento web: landing pages, automações, dashboards e manutenção de sistemas.

**No ar:** https://GuilhermeLuizatto.github.io/portfolio/

Duas peças, cada uma num **único arquivo HTML** — sem build, sem framework, sem back-end.
Dá para baixar e abrir com duplo clique.

| Peça | Abrir | Código |
|---|---|---|
| **Página de serviços** — landing page completa, do briefing à entrega | [ver](https://GuilhermeLuizatto.github.io/portfolio/lp-servicos/) | [`lp-servicos/index.html`](lp-servicos/index.html) |
| **Calculadora da reforma tributária** — CBS e IBS ano a ano, 2026→2033 | [ver](https://GuilhermeLuizatto.github.io/portfolio/calculadora-reforma-tributaria/) | [`calculadora-reforma-tributaria/index.html`](calculadora-reforma-tributaria/index.html) |

---

## Página de serviços

Landing page construída em etapas fixas: briefing, estratégia de conversão, copy, direção de
arte, desenvolvimento, testes e entrega. O movimento é guiado pela rolagem, com um palco fixo
onde o processo passa etapa por etapa e termina abrindo em leque nos quatro testes.

Decisões técnicas que valem a leitura:

- **Zero dependência externa.** Nada de GSAP nem de CDN: reveal, parallax e o traço que se
  desenha saem de CSS scroll-driven e de um kit de movimento de 4 KB embutido no arquivo. O
  motivo é prático — a página precisa abrir do disco, porque vai anexada a propostas.
- **Cor calculada, não escolhida no olho.** As quatro cenas de cor foram definidas em OKLCH e
  cada combinação de texto e fundo teve o contraste conferido por cálculo antes de uma linha
  de CSS ser escrita. O laranja forte nunca é usado como corpo de texto sobre o papel, porque
  dá 3,43:1 — só em título grande e borda.
- **Mobile mais leve que o desktop.** Num celular com a CPU limitada a 1/4, a rolagem estava
  em 46 FPS. Um teste A/B isolou a causa (a transição de cor repintando a viewport inteira,
  não o marquee, que era o palpite óbvio) e o ajuste levou para 52 FPS.
- **Funciona sem JavaScript**, inclusive as cores: cada seção pinta a própria cena.
- **Nada inventado.** Nenhum depoimento, número de clientes, selo ou logo. A página diz isso
  em voz alta, e é a mesma regra que vale para o trabalho de cliente.

Cada peça tem briefing e relatório de entrega escritos antes e depois do código, com a direção
de arte, o roteiro de movimento e os resultados dos testes. Eles não estão neste repositório
por serem documentos internos, mas eu mostro numa conversa se você quiser ver como o processo
funciona por dentro.

## Calculadora da reforma tributária

Simula, ano a ano de 2026 a 2033, quanto uma empresa de serviços recolheria de tributos sobre
consumo no modelo atual e no da CBS e do IBS. Trata Lucro Presumido e Simples Nacional de
formas diferentes, porque o Simples continua existindo depois da reforma: ali a conta compara
ficar com sair, não soma os dois.

A decisão de projeto que importa: **nenhuma alíquota está escondida no código.** Todas ficam
num painel editável, marcadas como estimativa a confirmar na fonte oficial, porque a alíquota
de referência ainda não foi fixada. Uma calculadora tributária que finge certeza sobre um
número que o Senado ainda não definiu é pior que calculadora nenhuma.

O gráfico é SVG gerado na mão — não há biblioteca de 300 KB para desenhar oito barras. Nenhum
dado sai do dispositivo: não há back-end, cookie nem analytics.

---

## Rodar localmente

Abrir direto, sem servidor:

```powershell
start .\lp-servicos\index.html
```

Servir em HTTP (necessário para Lighthouse ou para os scripts de teste):

```powershell
npx --yes serve . -l 4173
```

## Se você renomear o repositório

As três páginas trazem a URL canônica apontando para um repositório chamado `portfolio`. Se
der outro nome, rode isto na raiz do repositório para corrigir as três de uma vez:

```powershell
Get-ChildItem -Recurse -Filter index.html | ForEach-Object { (Get-Content $_.FullName -Raw) -replace 'GuilhermeLuizatto\.github\.io/portfolio', 'GuilhermeLuizatto.github.io/NOVO-NOME' | Set-Content $_.FullName -Encoding utf8 }
```

Troque `NOVO-NOME` antes de rodar. O mesmo vale se você passar a usar domínio próprio: nesse
caso substitua o host inteiro.

## Publicar no GitHub Pages

```powershell
git init; git branch -M main; git add .; git commit -m "Peças de portfólio"
```

Crie o repositório no GitHub (público, **sem** README, .gitignore ou licença, porque já
existem aqui), e depois:

```powershell
git remote add origin https://github.com/GuilhermeLuizatto/portfolio.git; git push -u origin main
```

No GitHub: **Settings → Pages → Source: Deploy from a branch → Branch: `main` / `(root)`**.
O endereço fica no ar em um ou dois minutos.

O arquivo `.nojekyll` já está aqui: ele impede o GitHub Pages de rodar o Jekyll, que ignora
arquivos e pastas começados por `_` ou `.`.

---

## Contato

WhatsApp [13 99664-9260](https://wa.me/5513996649260) ·
[guilhermeluizatto@gmail.com](mailto:guilhermeluizatto@gmail.com) ·
[github.com/GuilhermeLuizatto](https://github.com/GuilhermeLuizatto)

Também mantenho o [Atendara](https://atendara.app), um SaaS de agendamento em produção, e sou
um dos três desenvolvedores da [Serifa Labs](https://serifalabs.com).
