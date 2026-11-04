# Validação da base 2.0.0

Implementação nova em `forgeon/`, sem importação de código ou banco do ERP anterior.

## Verificado

- Ambiente virtual novo com apenas dependências declaradas; `pip check` sem conflitos.
- 32 testes locais Linux aprovados: 31 distribuídos e um teste privado adicional de
  compatibilidade com planilhas Shopee. Nenhum dado ou fixture privado acompanha o ZIP.
- Dez páginas em banco vazio e com dados sintéticos; entrada/saída do event loop Qt.
- Produtos canônicos e vínculos de anúncios/SKU; normalização não confunde Sonic e Super Sonic.
- Cálculo decimal de custos, embalagem, energia, máquina e preço, com valores inválidos recusados.
- Reservas concorrentes de SKU; códigos não reaproveitados; conflito entre produtos em vermelho.
- Importação transacional de pedidos; falha reverte a operação inteira. Reimportação não duplica
  nem apaga pedidos ausentes do arquivo. Correções manuais de SKU persistem nas reimportações.
- Resumo Shopee separado dos pedidos; cobertura mensal e dados parciais identificados.
- Cancelamentos e devoluções no consumo; relatórios de resultado não são conciliação bancária.
- Backup SQLite consistente, restauração com backup prévio, rejeição de bancos não reconhecidos.
- Exportações Excel com células de texto explícitas, evitando executar fórmulas em nomes importados.
- Leitura limitada de 3MF/G-code; XML com entidades não permitido; nenhum comando é enviado.
- Limites de tamanho para arquivos e recusa de macros/vínculos externos em XLSX.
- Análise estática da fronteira: runtime sem módulos de rede, subprocessos, navegador,
  avaliação dinâmica de código, extensões, MCP ou dependências da aplicação antiga.
- Wheels oficiais para Windows x64/Python 3.12 baixados com verificação dos hashes do requirements.

## Ainda depende do computador Windows

- Execução real dos lançadores CMD, instalação inicial e apresentação gráfica em sua resolução/DPI.
- Verificação do ZIP pelo Microsoft Defender. Não há laudo antivírus ou assinatura de executável.
  Os testes e a revisão não garantem ausência de detecção ou vulnerabilidades.

## Reproduzir

Com dependências instaladas, na pasta do projeto:

```text
python -m unittest discover -s tests -v
```

Em Linux sem monitor, defina `QT_QPA_PLATFORM=offscreen`.
A validação privada de planilhas não é necessária para executar o programa.
