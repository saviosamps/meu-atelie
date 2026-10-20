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

## Proteção contra dados corrompidos
- Se o conteúdo da chave `meuAtelie_v1` não puder ser lido ou validado (JSON ilegível, listas ausentes, registros inválidos, identificadores repetidos), o `index.html` entra em **modo protegido**:
  - nenhuma gravação é feita na chave `meuAtelie_v1`; cadastro, edição, exclusão e exportação ficam bloqueados;
  - o conteúdo original é copiado, sem alteração, para uma chave nova `meuAtelie_v1_copia_<data e hora UTC>` (ex.: `meuAtelie_v1_copia_2026-10-20T04:57:02.626Z`). Cópias existentes nunca são sobrescritas nem apagadas; se já houver uma cópia idêntica, ela é reaproveitada;
  - se a cópia não puder ser criada (ex.: armazenamento cheio), o aplicativo continua bloqueado, informa o motivo e oferece "Tentar criar a cópia novamente";
  - "Baixar conteúdo original" baixa o conteúdo exatamente como está salvo, em um arquivo `.txt`;
  - para sair do modo protegido, use "Recuperar a partir de um backup". É preciso ter a cópia criada, o backup precisa ser válido e a substituição é confirmada antes.
- Antes de cada gravação, o app confere se o conteúdo salvo continua igual ao lido por esta aba. Se outra aba ou janela tiver alterado os dados, nada é salvo, as gravações desta aba são bloqueadas e aparece a opção de recarregar a página.
- O `molde.html` apenas lê os dados. Se estiverem ilegíveis, ele avisa e permite informar as medidas manualmente.
- Limitação: o download é gravado em UTF-8; caracteres inválidos isolados (raros) podem ser substituídos no arquivo, mas a cópia no navegador é idêntica ao original.

## Gerador de moldes
- Ao escolher uma cliente, os campos são preenchidos apenas com as medidas cadastradas dela: `cintura`, `quadril`, `saia` e `cinturaQuadril`. Medidas não cadastradas ficam em branco e são listadas no aviso. A altura cintura–quadril usa o padrão de 20 cm.
- A opção "Informar medidas manualmente" limpa os campos.
- Trocar de cliente ou alterar uma medida descarta a prévia anterior. É preciso gerar novamente antes de imprimir.
