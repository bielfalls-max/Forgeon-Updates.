# Forgeon Studio ERP 2.0

Aplicativo desktop de gestão de impressão 3D, reimplementado do zero em Python/Qt.
Começa com banco vazio e não lê a instalação antiga. Nenhum código da extensão,
MCP, criação de anúncios, edição de fotos ou automação de navegador foi incluído.

## Instalação Windows

1. Verifique o ZIP com o Microsoft Defender, mantendo a proteção ativa.
2. Extraia em uma pasta nova, por exemplo `Documentos\Forgeon 2.0`.
3. Tenha o **Python 3.12 64 bits**, com o Python Launcher (`py`), instalado de
   [python.org](https://www.python.org/downloads/windows/).
4. Execute `INSTALAR_DEPENDENCIAS.cmd` uma vez. Ele cria um ambiente `.venv` novo
   e instala apenas Qt Widgets, leitor de Excel e parser XML do PyPI oficial.
   É necessário acesso à internet nessa etapa. Não precisa de administrador.
5. Abra `ABRIR_FORGEON.cmd`. Pode criar um atalho desse arquivo na Área de Trabalho.

Não instale por cima do Forgeon antigo. A instalação não usa o `.venv` anterior.
Não utiliza PowerShell, ExecutionPolicy Bypass, VBS, serviços, tarefas agendadas,
execução remota ou autoatualização. O uso normal funciona sem internet.

Dados novos ficam em `%LOCALAPPDATA%\Forgeon2\forgeon2.sqlite3`.
Para um ambiente de teste isolado, defina `FORGEON2_HOME` para outra pasta.
O aplicativo permite apenas uma janela por pasta de dados. O programa pode
ficar em Documentos sem depender do nome do usuário do Windows.

## Funções

- **Produtos:** um cadastro por boneco, custos, horas, peso e cores/gramas.
  Anúncios/SKUs diferentes apontam para o mesmo produto e compartilham custos.
  Normalização conservadora de nomes; Sonic e Super Sonic continuam separados.
  Arquivar preserva os pedidos e o custo usado nos relatórios atuais.
- **Precificação:** filamento, energia, máquina/hora, embalagem, outros custos,
  custo manual opcional, taxa percentual, taxa fixa e acréscimo sobre custo.
- **SKUs e vínculos:** catálogo, reserva manual/próximo número, zeros à esquerda,
  códigos não reutilizados automaticamente e conflito em vermelho quando
  importações usam um SKU para personagens diferentes. Correções ficam no histórico.
- **Impressão:** lê metadados de 3MF fatiado Bambu/Orca ou G-code para preencher
  gramas, cores e tempo. Escolha a placa e quantas unidades do mesmo produto ela
  contém. Projetos sem dados de fatiamento são recusados. Não comanda impressoras.
- **Pedidos:** lista mensal, detalhes e cadastro manual de um item por pedido.
- **Importação Shopee:** prévia de XLSX, confirmação e backup anterior. Pedidos
  combinados por ID; reimportar atualiza apenas os IDs presentes. Outros pedidos,
  custos, cores e correções de SKU são preservados. O arquivo deve conter todas
  as linhas dos pedidos presentes: reimportar um ID substitui seus itens.
- **Estatísticas:** resumo pago e produtos por anúncio em área separada. O resumo
  nunca é somado aos pedidos, nem usado para inventar SKUs ou consumo por cor.
- **Financeiro:** despesas e compras de filamento; compras não são descontadas
  duas vezes como custo de material no resultado.
- **Relatórios:** vendas detalhadas, taxas, resultado operacional estimado,
  caixa operacional estimado, mais vendidos, consumo por cor/mês/quinzena,
  compras mensais e resumo Shopee. Exportação Excel sem macros.
- **Planilhas:** exportação de produtos, SKUs, pedidos, financeiro e relatório;
  geração de modelo vazio de pedidos compatível com a importação.
- **Backup:** banco SQLite consistente, integridade verificada, restauração de
  backups do Forgeon 2 com backup prévio. Não aceita banco do aplicativo antigo.

## Regras que evitam resultados incorretos

`Order.toship` é apenas A Enviar. Para todas as variações, importe **Todos os
pedidos (`Order.all`)**. Um resumo de estatísticas não informa variações.
Resultados ficam PARCIAIS sem cobertura mensal conferida ou custos preenchidos.

Os relatórios usam o **cadastro de custos atual**, não custos históricos congelados.
Caixa é uma estimativa operacional pelos pedidos, não o saldo bancário. Devoluções
reduzem unidades/consumo, mas reembolsos precisam de conciliação e são sinalizados.
As taxas vêm da planilha; parâmetros de precificação não atualizam automaticamente
as regras comerciais da Shopee. Confira seus percentuais em Configurações.

O leitor não armazena nomes, CPF, endereços ou telefones de compradores. Somente
campos de gestão dos produtos/pedidos são persistidos. Nenhuma planilha do usuário,
banco pessoal, senha ou token é incluído na distribuição.

## Validação e limites

Testes automatizados de banco, cálculos, importação/reimportação, SKUs, relatórios,
backup/restauração e UI executados em Linux. A execução real dos dois lançadores
no Windows precisa ser confirmada no seu computador. O pacote não tem certificado
de assinatura nem laudo antivírus. Reimplementação e testes não substituem essa análise.

Esta é uma nova base 2.0.0: sem migração de dados antigos por escolha do usuário.
