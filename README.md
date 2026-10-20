# meu-atelie
Aplicativo de modelagem e gestão de costura

## Arquivos
- `index.html`: cadastro de clientes, medidas e peças, além de exportar e importar backup.
- `molde.html`: gerador experimental de molde de saia reta para imprimir em folhas A4.

## Dados
- Os dados ficam no navegador (`localStorage`, chave `meuAtelie_v1`). Não há sincronização entre dispositivos: use **Exportar/Importar backup**.
- O nome da cliente é obrigatório e não pode conter apenas espaços.
- Ao abrir o app ou importar um backup, os dados são verificados **sem alteração**:
  - clientes sem nome continuam salvos, aparecem como "Cliente sem nome" e geram um aviso na tela. Para corrigir, use "Editar medidas";
  - um backup com registros em formato inválido (sem identificador, identificador repetido, arquivo que não é JSON) é recusado com uma mensagem, e os cadastros atuais não mudam.

## Gerador de moldes
- Ao escolher uma cliente, os campos são preenchidos apenas com as medidas cadastradas dela: `cintura`, `quadril`, `saia` e `cinturaQuadril`. Medidas não cadastradas ficam em branco e são listadas no aviso. A altura cintura–quadril usa o padrão de 20 cm.
- A opção "Informar medidas manualmente" limpa os campos.
- Trocar de cliente ou alterar uma medida descarta a prévia anterior. É preciso gerar novamente antes de imprimir.
