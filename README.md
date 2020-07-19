# snownews_improve
Script para melhorar snownews, com opção de favoritos e suporte para https.


## Descrição
Esse projeto fornece scripts em bash para melhorar a usabilidade do __snownews__. Como opções de favoritar o RSS, que é armazenado em um feed de favoritos. Outra funcionalidade é a instrução para suporte a _https:_.

### Por que usar __snownews_improve__?
Devido a sua alta simplicidade, os scripts permitem enorme adequação a suas necessidades, como (a) baixar um determinado dado de um conteúdo da página do rss, (b) baixar e salvar a página em formato pdf para posterior leitura, (c) entre outras inumeras possibilidades. __O céu é o limite__ xD

### Como adequar ao meu uso?
Para isso basta construir um __shellscript__ com sua necessidade e incorporar aos scripts padrões do __snownews_improve__, seja com chamada de função ou mesmo adicionando as funções no arquivo padrão.


## Modo de Ação
### Geral
Os scripts são armazenados em um diretório _scripts_ localizado em _~/.snownews/_.

### Https
Para suporte para _https:_ o projeto não apresenta nenhuma inovação, apenas orienta para utilização do __lynx -source__ ou __curl__ (ou mesmo __curl -k__) para estabelecer uma conexão TLS com o servidor.

Exemplo de edição do arquivo _~/.snownews/urls_:
>
> exec:lynx -source 'https://example.com/feed/content.rss'|Titulo_rss|Grupo_rss|
>

_Obs: O mantenedor utiliza e mantem o __lynx__ por escolha pessoal, visto que alguns servidores impedem a conexão com __curl__ sem __-user-agent__ reconhecido pelo servidor._

### Favoritos
Scripts são divididos em arquivos separados para facilitar o manutenção. Composto por 03 frentes:
- _fav_read.sh_ (construção de um rss com os favoritos);
- _fav_new.sh_ (adição de um novo rss aos favoritos);
- _fav_del.sh_ (deleta um rss favorito).

Os \<item\> dos link que deseja favoritar é selecionado e armazenado em um arquivo dentro de um diretório chamado _favorites_ dentro do diretório padrão do __snownews__.

### Pré-visualização
O usuário pode construir scripts que filtram o conteúdo do feed de acordo com o domínio do site. A pré-visualização é chamada pelo o script _preview.sh_ que define o domínio do site e direciona para o script de filtragem contido no diretório _~/.snownews/scripts/previews.d_. Dentro deste diretório se encontram scripts específicos de filtragem como _~/.snownews/scripts/previews.d/nature.sh_ que filtra o conteúdo dos feeds do <feed.nature.com>:

>
> FILE\_TEMP=/tmp/snownews.temp.html
> LINK="$1";
>
> echo '<meta charset="UTF-8">' > $FILE\_TEMP;
>
> lynx -source "$LINK" \
>        | tr '\n' ' ' \
>        | sed 's/<div class="article/\n<div class="article/g' \
>        | grep -m 1 '\_\_body ' \
>        | sed 's/href="/id="/g' >> $FILE\_TEMP;
>
> lynx $FILE\_TEMP;
>


## Instação
Para as melhoras do __snownews__ utilize o _install.sh_ do projeto.


## Dependências
Dependencias dos scripts, podem ser alterados com a edição dos scripts:
- snownews (obviamente);
- lynx.


## Versões
### Versão 1.0
Suporte:
- https (exemplo de uso);
- favoritos (adição / leitura / deleção).


## Mantenedor
Vinicius D Sartori Rimoldi  <viniciusrimoldii@gmail.com>


## Licença
Licenciado por GpL-v3.


## Suporte e Bugs
Favor enviar erros, bugs e sugestões de melhora para o email do mantenedor (<viniciusrimoldi@gmail.com>).

