# EntregaJá CG: por que o cancelamento subiu?  (modelo de README)

> Copie este arquivo para o seu repositório como README.md e preencha cada seção com as SUAS palavras e números.

## 1. Contexto
Uma frase sobre a empresa fictícia e o problema que o CEO pediu para investigar.
"Os cancelamentos estão subindo e os clientes reclamam de demora. Não sei onde está o problema, nem quanto isso nos custa. Quero saber o que está acontecendo, com números, e o que fazer a respeito. Você tem três semanas."
## 2. Dados
Tabelas usadas, período e tamanho. Aviso: dados fictícios, gerados para estudo.

## 3. Auditoria e limpeza dos dados
| Problema encontrado | Como encontrei (consulta) | Decisão tomada e por quê | Linhas afetadas |
|---|---|---|---|
| ... | ... | ... | ... |

## 4. Perguntas e descobertas
Para cada pergunta: a conclusão em uma frase, o número que a sustenta e o link para a consulta.
1. ...

## 5. Dashboard
Imagens (prints) do Power BI/Excel e uma linha explicando o que cada visual mostra.

## 6. Recomendações
Três ações, cada uma com o número que a justifica e o impacto esperado.

## 7. O que errei e o que aprendi
Pelo menos dois erros reais do processo (ex.: soma duplicada por JOIN) e como corrigi.

## 8. Como reproduzir
Ordem dos scripts e ferramentas (PostgreSQL, Power BI...).

## 9. Transparência
Enunciado e dados gerados com apoio de IA. Consultas, análise e conclusões escritas por mim.
<!-- ##
Aqui eu vou tentar minha resolução e pensamentos do problema e similares
Adicionando enfim de deixar tudo as claras, eu utilizo IA para tirar duvidas e tentarei deixar explicito como utilizei-a 

-Primeiramente fui transformar os dados para ver se eles estavam/vieram formatados de forma correta em ,clima diário,a chuva em mm veio em número inteiro e a temp maxima também veio em número inteiro,porém vejo um problema pois não faz sentido obviamente temp de 317,dito isto alterei a temp max para localidade ingles-us com numero decimal , ficando da seguinte forma data 2026-03-01 , chuva mm 9.8,  temp_max 31.7 , mas pensando aqui talvez so alterar a localidade para ingles-us,já resolveria? Continuando na tabela pedidos eu altererei valor itens,taxa entrega para tipo decimal com localidade us para fins de padronização,em desconto esta formatado como texto porém mudar para porcentagem( correto),mas qual pode ter algum impacto futuro em alguma formula? estarei mudando temporariamente para porcentagem,tive um problema mudei para porcentagem e ficou 5000%,olhei no arquivo .csv e está 5.00, usando uma pesquisa  com IA para encontra o erro mais rápido eu cometi o erro de analisar de forma errada aparentemente não é um valor de desconto em porcentagem é um valor que vai ser descontado direto,como na shoppe por exemplo que ele desconta um valor direto,então alterei para decimal para fim de padronização e percebi logo de cara que um valor ficou 9,15 e fui cego de mais em querer mudar direto porque a coluna anterior tem a parte de cupons que coincide com o exemplo da SHOPEE ,olhando mais a frente na tabela alterei o tempo entrega min para valor inteiro, e alguns valores deram null devido o pedido ser cancelado então alterei os valores nulos a 0 para não dar algum problema na montagem gráfica (pra mim no momento faz sentido mas talvez seja overthinking,que nem sempre é necessário ),obs alguns pedidos não entregues(cancelados)ficaram sem nota e alguns pedidos ficaram sem nota, a ver o impacto.Enfim na ultima tabela (restaurantes), eu mudei para numero decimal -US para fins de padronização de novo , sim k,eu acho que isso pode facilitar na montagem de gráficos por algum acaso.Agora fechei e apliquei esses dados transformados a princípio
Feito depois,fiz denovo o erro de ler o "briefing" depois e percebi que podia ter outros erros de Letra por exemplo que eu esqueci de formatar(preguiça) devido ao tamanho das tabelas portanto, rapidamente entre as tabelas filtrei para ver se tinha valores maiores que o padrão ou valores exorbitantes, e na tabela pedidos o bairro_entrega verifiquei q repetia varios bairros,tirando dúvida com IA ,estava tentando substituir valores por exemplo   Monte CASTELO,MONTE CASTELO e similares por Monte castelo,mas não estava fazendo então entendi que havia uma maneira simples.que o a aba transformar utilizando a "função" formato eu poderia transformar tudo em maiúsculo por exemplo para depois deixar as iniciais em maiúsculo ,reduzindo uma etapa e depois cortar que removeria eventuais espaços entre eles,com isso feito olhei o filtro e não houve nenhum bairro repetido,
na coluna seguinte visualizei que os valores itens em valor decrescente superou 10k ou seja meio impossivel,tirei duvida novamente com IA, para saber se tem como descobrir que o valor poderia ser 170,11 em vez de 17011 pois pode ser que de onde veio os dados não veio com a padronização quando formatei os dados por valor decimal(INGLES-US),então me sugeriu verificar o ticket médio do restaurante,então fiz uma medida simples copiei todo o dax do ticket médio e fiz que o valor do pedido seja menor que 500 , e filtrei pelo id do restaurante correspondente(1º verifiquei o id=3(sushi), 2º id=13=churrasco),logo assumi que não é impossivel mas é plausível um valor de 170 para sushi e 150 para churrasco,enão substui os valores por 170 e etc,e filtrei por ordem crescente e tinha valor com - , então substui também,formatei o status seguindo exemplo de bairro_entrega,com isso finalizado olhando as outras tabelas o resto parece OK,

Para começar eu devo descobrir o faturamento direto,mas como meu conhecimento é básico no power BI, eu pensei o seguinte em utilizar medidas rápidas para fazer o faturamento da seguinte forma:

pegar o valor dos itens e depois subtrair do desconto
dps outra medida rápida do resultado da medida acima e somar com taxa de entrega
porém confirmando com a IA que o resultado seria correto ela sugeriu utilizar o calculate para deixar toda medida em 1,então agora está caculate que soma a taxa de entrega com o valor dos itens e subtrai pelo desconto e tem que deixar apenas os pedidos que estão como entregues porque caso contrário estaria contando um dinheiro "fictício" que nunca vai entrar (provavelmente)
Prosseguindo a montagem do dashboard eu não tenho familiaridade com montagem de dashboards então utilizarei um template
Estava pensando em tentar montar uma relação com a tabela clima diário já que ela estava IA, então acabei perguntando para IA, mas nem precisava, fui em transformar dados e adicionei uma nova coluna de somente data(data_horas) da tabela pedidos e então transformei dados e fiz a ligação entre data(clima diário) e Data(pedidos),além disso fiz uma:
* matriz para ver quais bairros recebiam mais entregas por tipo de veículo(moto,bicleta)
* um gráfico de rosca para a forma de pagamento
*um tabela de faturamento por bairro
*Slider por temperatura(meio inútil)
*Filtro por MM de chuva( difícil fazer uma análise mais profunda com dados fictícios)
*Filtro por nota do cliente 
* Gráfico de rosca por meio do pedido (instagram,indicação,acho difícil fazer com os dados atuais por que por exemplo nem sempre quem pede fala por exemplo por onde ele fez a compra )
* Um gráfico que faz Bairro onde foi feita a entrega vs Categoria Vs Faturamento(sinceramente meio de mais,acho que não precisava , eu poderia ter feito um gráfico no lugar por exemplo de apenas categoria que os outros visuais iriam se adaptar)

*OBS:Aqui está um arquivo de "exigências" pedidas,porém houve um vacilo por minha parte, nao tinha visto antes de começar o projeto
Utilizando a página 2 para isso,fui utilizar o cartão visual KPI pois eu achava que ele seria ideal para Key Performance Indicator mas fiz 2 Kpi de Faturamento e pedi para IA verificar se tinha erros,logo notei que havia erros e pedi para consertar pois eu estava tentando utilizar o KPI,tentei filtrar por valor maior que 0 ou não nulo no próprio filtro e não estava chegando ao resultado então tive que perguntar para IA se eu estava cometendo algum erro e onde, então fiz por Medida mesmo mas acabei vendo um exemplo da IA e não consegui desver,então adicionei na medida do média do tempo de entrega onde o pedidos tem que ter tempo de entrega >0 e menor que 999,mas ajustei para menor que 300 pois 5 horas já é mais do que necessário para essa métrica
Página 2 (Resolução do "brifieng" feito pela IA , arquivo PDF)
*Ticket médio, é copiar o faturamento e dividir pela qntd de pedidos entregues
*Média do temp de entrega(average temp_entega_min e maior que 0 e menor que 300(5 horas ))

 -->