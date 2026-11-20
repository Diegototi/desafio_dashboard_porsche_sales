# desafio_dashboard_porsche_sales
Desafio DIO. Criando dashboard de vendas com modelos de carros da Porsche.

  Desenvolvi este dashboard como parte do desafio do curso **Criando Agentes de Tratamento de Dados**, da [DIO](https://www.dio.me/). Na prática, utilizei Inteligência Artificial para manipular uma planilha e transformar dados brutos em uma base limpa e sanitizada. Em seguida, construí o dashboard para centralizar os principais indicadores (KPIs) em uma única tela, facilitando o acompanhamento de metas e a tomada de decisões rápidas.

  
<br>  
<br>
<br>
<p align="center">
  <a href="#bar_chart-tratando-a-base-de-dados">Tratando a base de dados</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp; 
  <a href="#question-perguntas-de-negócio">Perguntas de negócio</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#bulb-prompt-e-ferramentas-do-dashboard">Prompt e ferramentas do dashboard</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#frame_with_picture-imagens-e-exemplos-de-filtros">Imagens e exemplos de filtros</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#memo-license">Licença</a>
</p>
<br>

### :bar_chart: Tratando a base de dados

A base de dados consiste em uma planilha com o histórico de vendas de veículos **Porsche** ao longo de vários anos, contendo as seguintes colunas: `ID`, `vendedor`, `comprador`, `cidade`, `estado`, `modelo`, `ano de fabricação`, `preço` e `status da venda`.

Para corrigir inconsistências e padronizar informações (como datas, moedas, nomes de cidades e modelos), utilizei o **Claude** (versão gratuita) seguindo este fluxo:

1. **Definição de regras (`schema.md`):** Criei um arquivo de especificações contendo as regras e exemplos de formatação esperada para cada coluna.
2. **Processamento com IA:** Enviei a planilha bruta junto com o arquivo `schema.md` para o Claude utilizando o seguinte prompt:

```text
Crie um agente que leia o arquivo Planilha Porsche.xlsx e aplique as regras do schema.md para gerar um novo arquivo tratado.
```

3. **Saída e automação (`porsche.py`):** O Claude retornou a planilha já sanitizada e gerou um script em Python (utilizando a biblioteca `openpyxl`). O código lê o arquivo `.xlsx`, cria colunas *"Sanitized"* ao lado das originais, marca valores fora do padrão como `INVALID` e gera uma aba de log detalhando todas as alterações.
4. **Validação final:** Após revisar o log e realizar pequenos ajustes manuais, a base ficou pronta para alimentar o dashboard.
5. **Segurança e privacidade dos dados:** Antes de gerar o HTML do dashboard, utilizei o Claude para remover as colunas com dados pessoais (`vendedor` e `comprador`) e auditar o arquivo final, garantindo que nenhuma informação sensível fosse exposta. Após a confirmação da IA, realizei uma verificação manual final.

```text
Prompt 1 (Anonimização):
Remova da planilha os nomes dos vendedores e compradores e me informe se julgar alguma outra informação de segurança para remover.

Prompt 2 (Auditoria):
Confirme com certeza e provas que os nomes dos vendedores e compradores que estavam na planilha base não foram parar no HTML final.
```
<br>
<br>
<br>

### :question: Perguntas de negócio

* **Indicadores de topo, como total de vendas e receita** - Permitem uma visão rápida do desempenho comercial, facilitando o acompanhamento do volume de vendas e do faturamento gerado. Funcionam como indicadores de referência para avaliar os resultados gerais do negócio.
* **Modelos campeões de vendas** - Destaca os veículos com maior volume de vendas no período analisado, permitindo identificar os modelos de melhor desempenho comercial e compreender quais produtos concentram maior participação nas vendas.
* **Total de venda geral e por ano** - Permite identificar quais modelos possuem maior demanda em cada período, acompanhar mudanças nas preferências dos consumidores e analisar tendências de vendas ao longo dos anos, contribuindo para decisões de estoque e planejamento comercial.  
* **Modelos mais vendidos por cidade** - Permite comparar o volume de vendas entre cidades, identificar mercados com maior relevância comercial e analisar o desempenho regional, apoiando decisões de expansão e estratégias de atuação local.

**Interatividade e indicadores de desempenho**

Todos os indicadores e análises possuem representações gráficas e podem ser explorados por meio de filtros interativos de Ano da venda, Cidade e Forma de pagamento, permitindo segmentar os dados e comparar diferentes cenários. A dashboard apresenta quatro indicadores principais:
<br>
*Volume de vendas: quantidade total de vendas realizadas.*
<br>
*Receita bruta: valor total gerado pelas vendas.*
<br>
*Ticket médio: valor médio por venda.*
<br>
*Entregues: quantidade de veículos com entrega concluída.*
<br>
<br>
<br>

### :bulb: Prompt e ferramentas do dashboard

Nesse desafio, utilizei o **ChatGPT** (versão gratuita). Cheguei a fazer testes na criação de agentes, mas o resultado que mais me agradou foi utilizando o chat tradicional combinado com o recurso **Canvas**. 

Veja o prompt inicial utilizado para gerar a estrutura:

```text
Utilizando o recurso canvas, renderize um dashboard em HTML. Crie indicadores de topo, como total de vendas e receita.

# Filtros:
-> Modelos mais vendidos por ano
-> Modelos mais vendidos por cidade
-> Modelos vendidos por forma de pagamento

# Perguntas de negócio e KPIs:
-> Total de venda geral e por ano (com gráfico)
-> 5 modelos campeões de vendas (com gráfico)
-> Campeões de vendas por cidade (modelos, ano e valor com gráfico)

Sobre o UI/UX, baseie-se no site oficial da Porsche Brasil (https://www.porsche.com), mantendo um ar elegante e sóbrio.
```
**Ajustes e finalização:**
Após visualizar e conferir a primeira versão do dashboard, utilizei o seguinte prompt para ajustes visuais, formatação de dados e correções nos gráficos:

```text
- Adicionar no topo a foto de um carro Porsche
- Nos campos onde aparecem valores, mantenha o padrão com duas casas decimais após a vírgula sem arredondamento, nesse padrão: "Receita bruta \$12.827.800,50"
- Alguns gráficos estão cortando informações, por exemplo "Formas de pagamento - Quantidade por forma de pagamento" e "Desempenho por cidade - Ranking por volume · modelo, ano e valor". Pode escolher um gráfico melhor e/ou ajustar
```
<br>
<br>
<br>





### :frame_with_picture: Imagens e exemplos de filtros
Abra o projeto e instale as dependências e rode o projeto:

cd imhere <br>
npm install <br>
npx expo start <br>

### :wrench: Tecnologias | Ferramentas | Recursos

Esse projeto foi desenvolvido utilizando os seguintes recursos:

- [Vs Code](https://code.visualstudio.com/download);
- Visual Studio Code
- Android Studio
- Javascript
- NodeJS
- Expo
- React
- React Native
- TypeScript
- NPM

### :memo: License
Esse projeto está sob MIT license. Veja [LICENSE](https://github.com/Diegototi/series-console-app/blob/main/LICENSE) para mais informações.

---

Feito por Diego Almeida :blue_heart: Contato: https://www.linkedin.com/in/diego-almeida-a8394a215 :blush:
