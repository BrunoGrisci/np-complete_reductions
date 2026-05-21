# np-complete_reductions

<p align="right">
  <a href="README.md">English</a> |
  <strong>Português (Brasil)</strong>
</p>

**np-complete_reductions** é uma ferramenta educacional interativa, executada no navegador, para visualizar reduções clássicas em **tempo polinomial** usadas em provas de **NP-completude**.

A ferramenta foca em reduções de **SAT** e **3SAT** para problemas clássicos em grafos e aritmética. Ela mostra como fórmulas fonte são transformadas em instâncias alvo, como as soluções correspondem nas duas direções e por que as construções são computáveis em tempo polinomial.

Ela foi projetada para uso em sala de aula em **Teoria da Computação**, especialmente no ensino de reduções depois do teorema de Cook-Levin e antes ou junto do catálogo clássico de problemas NP-completos.

🔗 **GitHub Pages:** https://brunogrisci.github.io/npcompletereductions  

🔗 **Repositório GitHub:** https://github.com/BrunoGrisci/np-complete_reductions

---

## ✨ Funcionalidades

### Funcionalidade principal
- Visualizações interativas de reduções clássicas em tempo polinomial:
  - `SAT ≤P 3SAT`
  - `3SAT ≤P CLIQUE`
  - `3SAT ≤P CONJUNTO INDEPENDENTE`
  - `3SAT ≤P SUBSET-SUM`
  - `3SAT ≤P VERTEX-COVER`
  - `3SAT ≤P HAMPATH`
- Aba de visão geral explicando a estratégia geral de provas de NP-completude:
  - pertencimento a NP,
  - escolha de um problema fonte NP-completo conhecido,
  - construção de uma redução em tempo polinomial,
  - prova das duas direções de correção,
  - limitação do tamanho e do tempo da construção.
- Mapa de reduções mostrando como as reduções implementadas se relacionam com SAT e 3SAT.
- Exemplos predefinidos para cada redução, incluindo fórmulas satisfatíveis e insatisfatíveis.
- Entrada definida pelo usuário com validação para sintaxe CNF e 3CNF.
- Verificação por força bruta para exemplos pequenos, usada apenas como verificador didático.

### Modo de construção passo a passo
- Cada redução tem um painel de **Construção passo a passo**.
- O botão **Iniciar** limpa a instância alvo.
- **Próximo** adiciona o próximo objeto ou gadget da construção.
- **Anterior** retorna ao estado de construção anterior.
- **Cancelar** sai do modo de construção e restaura a instância alvo completa.
- Cada passo inclui uma explicação focada sobre o objeto criado e por que ele é necessário na prova.

### Visualizações das reduções
- **SAT ≤P 3SAT**
  - trata cláusulas CNF de tamanho 1, 2, 3 e maior que 3,
  - mostra variáveis auxiliares e cláusulas de três literais geradas,
  - enfatiza equissatisfatibilidade, não equivalência lógica usando apenas as variáveis originais.
- **3SAT ≤P CLIQUE**
  - cria um vértice para cada ocorrência de literal,
  - agrupa vértices por cláusula,
  - desenha arestas de compatibilidade entre literais não contraditórios de cláusulas diferentes,
  - verifica cliques candidatos de tamanho `k`.
- **3SAT ≤P CONJUNTO INDEPENDENTE**
  - cria um vértice para cada ocorrência de literal,
  - adiciona arestas de triângulo dentro de cada grupo de cláusula,
  - adiciona arestas de contradição entre literais opostos em cláusulas diferentes,
  - verifica conjuntos independentes candidatos de tamanho `k`.
- **3SAT ≤P SUBSET-SUM**
  - constrói a tabela de dígitos com colunas de variáveis e colunas de cláusulas,
  - mostra linhas de atribuição `yi` e `zi`,
  - mostra linhas de enchimento `gj` e `hj`,
  - destaca por que o alvo tem a forma `11...133...3`,
  - explica por que não ocorrem carries.
- **3SAT ≤P VERTEX-COVER**
  - constrói arestas de variáveis e triângulos de cláusulas,
  - conecta vértices de literais de cláusula aos vértices de literais de variável correspondentes,
  - verifica coberturas de tamanho no máximo `K`,
  - torna explícita a convenção de verdade.
- **3SAT ≤P HAMPATH**
  - constrói gadgets dirigidos de variáveis e vértices de cláusulas,
  - mostra direções de travessia correspondentes a atribuições de verdade,
  - adiciona arestas de desvio para cláusulas satisfeitas,
  - permite inspecionar e selecionar manualmente um caminho.

### Verificação interativa
- Fórmulas fonte são verificadas quanto à satisfatibilidade quando pequenas o suficiente.
- Instâncias alvo são marcadas como instâncias SIM/NÃO de acordo com a redução.
- A ferramenta pode exibir uma solução alvo correspondente quando ela existe:
  - atribuição satisfatória,
  - clique,
  - conjunto independente,
  - subconjunto que soma o alvo,
  - cobertura por vértices,
  - caminho hamiltoniano.
- Usuários podem selecionar manualmente vértices de grafos, linhas do subset-sum ou nós do caminho hamiltoniano.
- Os verificadores informam se a seleção manual satisfaz as restrições do problema alvo.
- Soluções da fonte e do alvo são mostradas lado a lado quando apropriado.

### Interação com grafos
- Reduções baseadas em grafos permitem arrastar nós:
  - CLIQUE,
  - CONJUNTO INDEPENDENTE,
  - VERTEX-COVER,
  - HAMPATH.
- As arestas permanecem conectadas enquanto os nós são arrastados.
- Arestas inválidas selecionadas são destacadas nos verificadores relevantes.

### Usabilidade e apresentação
- Interface de página única com abas.
- Design visual limpo e adequado para projeção em aula.
- Alternância entre modo claro/escuro.
- Alternância entre Inglês e Português do Brasil.
- Preferências persistentes via `localStorage`:
  - tema,
  - idioma.
- Totalmente client-side, sem backend e sem framework externo de UI.

---

## 🧠 Objetivos pedagógicos

Esta ferramenta foi construída para ajudar estudantes a:

- ver reduções como transformações explícitas de instâncias, não apenas como diagramas de prova,
- conectar cada cláusula ou ocorrência de literal da fórmula fonte a um objeto na instância alvo,
- entender a diferença entre uma construção e um verificador por força bruta,
- inspecionar por que instâncias SIM são mapeadas para instâncias SIM,
- inspecionar por que instâncias alvo SIM implicam instâncias fonte SIM,
- entender o papel de gadgets, variáveis auxiliares, dígitos de enchimento e arestas de grafos,
- distinguir arestas de compatibilidade, arestas de conflito e arestas de cobertura em reduções diferentes,
- ver por que a instância alvo construída tem tamanho polinomial.

Ela é adequada para:

- disciplinas de graduação em Teoria da Computação,
- demonstrações em sala com projetor,
- exercícios guiados sobre reduções de NP-completude,
- estudo individual de problemas NP-completos clássicos,
- comparação de múltiplas reduções a partir do mesmo problema fonte.

---

## 📄 Modelo de entrada

A ferramenta aceita fórmulas no estilo CNF em vários formatos convenientes para sala de aula, por exemplo:

```text
(x1 v !x2 v x3) ^ (!x1 v x2 v x4)
(x1 ∨ ¬x2 ∨ x3) ∧ (¬x1 ∨ x2 ∨ x4)
x1,!x2,x3; !x1,x2,x4
```

Para `SAT ≤P 3SAT`, as cláusulas podem ter qualquer tamanho positivo.

Para as reduções a partir de `3SAT`, toda cláusula deve ter exatamente três ocorrências de literais. Ocorrências repetidas são permitidas, como em exemplos didáticos padrão:

```text
(x1 v x2 v x2) ^ (x1 v !x2 v !x2)
```

Para fórmulas pequenas, o verificador por força bruta embutido encontra uma atribuição satisfatória quando ela existe. Esse verificador aparece apenas para explicação e validação; ele não faz parte das reduções em tempo polinomial.

---

## 🌐 Internacionalização (i18n)

- Suporte completo a **Inglês** e **Português do Brasil**.
- Nomes de abas, controles, mensagens de validação, caixas de status, explicações da construção, provas e rótulos dinâmicos são bilíngues.
- Trocar o idioma **não** reinicia a fórmula atual, o exemplo escolhido, a aba selecionada, o estado da construção ou as seleções manuais.

---

## 🛠️ Stack tecnológica

- **HTML / CSS / JavaScript** puro
- Sem etapa de build
- Sem dependências externas
- Totalmente client-side
- Compatível com hospedagem estática, como **GitHub Pages**

Arquivos principais:

- `npcompletereductions.html`
- `assetsNPCompleteReductions/styles.css`
- `assetsNPCompleteReductions/script.js`

Para executar localmente, abra `npcompletereductions.html` diretamente no navegador ou sirva a pasta com qualquer servidor estático, por exemplo:

```bash
python3 -m http.server 4173
```

Então abra:

```text
http://127.0.0.1:4173/npcompletereductions.html
```

---

## 🧪 Verificação

O projeto é estático e não exige framework de testes. Durante o desenvolvimento, a implementação foi verificada com:

```bash
node --check assetsNPCompleteReductions/script.js
```

Também foi usada validação no navegador para confirmar:

- comportamento do parser para entradas CNF e 3CNF,
- exemplos satisfatíveis e insatisfatíveis para cada redução,
- preservação de respostas SIM/NÃO nas instâncias alvo construídas,
- comportamento de Iniciar / Próximo / Anterior / Cancelar no modo de construção,
- exibição de atribuições satisfatórias e soluções alvo,
- verificação manual de cliques e conjuntos independentes,
- seleção manual de linhas do subset-sum e conferência dos dígitos alvo,
- verificação manual de cobertura por vértices e destaque de arestas descobertas,
- verificação manual de caminho hamiltoniano,
- nós de grafos arrastáveis com arestas conectadas,
- alternância entre tema claro/escuro,
- alternância entre Inglês e Português do Brasil,
- legibilidade em telas desktop e mobile.

---

## 🚀 Trabalhos futuros (ideias)

- Adicionar um modo de aula guiado que avance automaticamente por cada construção.
- Adicionar anotações opcionais de prova ao lado de cada objeto construído.
- Exportar instâncias alvo geradas em formato legível por máquina.
- Adicionar mais exemplos de livros-texto e provas para cada redução.
- Adicionar uma visão complementar lado a lado para CLIQUE e CONJUNTO INDEPENDENTE.
- Adicionar screenshots e exemplos animados curtos ao README.

---

## 🎓 Créditos

**Desenvolvido por**  
**Prof. Bruno Iochins Grisci**  
Departamento de Informática Teórica  
Instituto de Informática – Universidade Federal do Rio Grande do Sul (UFRGS)  
🔗 https://brunogrisci.github.io/  
🔗 https://www.inf.ufrgs.br/site/  
🔗 https://www.ufrgs.br/site/

**Principal referência teórica**
- Michael Sipser, *Introduction to the Theory of Computation*, especialmente os capítulos sobre NP-completude e reduções de SAT/3SAT para problemas NP-completos clássicos.

**Contexto histórico**
- Richard M. Karp, “Reducibility Among Combinatorial Problems”, 1972.
- O trabalho de Karp introduziu o método de reduções em tempo polinomial como uma ferramenta central para demonstrar NP-completude de muitos problemas combinatórios hoje clássicos.
- A ferramenta usa versões didáticas padrão dessas reduções e prioriza clareza pedagógica em vez de codificações compactas.

**Nota de desenvolvimento**  
Esta ferramenta foi criada com assistência do **Codex GPT-5.5**.

---

## 📦 Licença

Este projeto está licenciado sob a **Licença MIT**.

Você pode usar, modificar e redistribuir para fins acadêmicos e educacionais, desde que haja a devida atribuição.

Veja o arquivo `LICENSE` para detalhes.

---

Se você usar esta ferramenta em ensino ou pesquisa, uma citação ou link para o repositório é bem-vindo.

## 📚 Citação

Se você usar esta ferramenta em trabalhos acadêmicos (artigos, teses, relatórios técnicos ou material didático), cite-a como:

```bibtex
@software{Grisci_NP_complete_reductions,
  author       = {Bruno Iochins Grisci},
  title        = {{np-complete\_reductions}: Um Visualizador Interativo de Reduções Clássicas em Tempo Polinomial},
  year         = {2026},
  url          = {https://github.com/BrunoGrisci/np-complete_reductions},
  note         = {Software educacional baseado na web},
}
```

---

## 🔄 Veja também

- **SAT-tableau**  
  Webtool: https://brunogrisci.github.io/sat_tableau  
  Repositório: https://github.com/BrunoGrisci/SAT-tableau

- **Gerador de Dominós TM → PCP (tm2pcp)**  
  Webtool: https://brunogrisci.github.io/tm2pcp  
  Repositório: https://github.com/BrunoGrisci/tm2pcp-webtool

- **Webtool PCP → Ambiguidade de GLC**  
  Web app: https://brunogrisci.github.io/pcp2cfg  
  Repositório: https://github.com/BrunoGrisci/pcp2cfg-webtool

- **Reduções executáveis de computabilidade**  
  Repositório: https://github.com/BrunoGrisci/reductions-computability
