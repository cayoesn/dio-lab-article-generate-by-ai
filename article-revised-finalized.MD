# Título: Conhecendo as Joias Escondidas do SQL: CUBE e ROLLUP

## Introdução
O SQL (Structured Query Language) é a linguagem padrão para gerenciamento de banco de dados relacionais,  muito utilizado para gravação de dados, atualização, deleção e principalmente consultas. Entre suas muitas funcionalidades, destacam-se duas pouco conhecidas, mas poderosas: CUBE e ROLLUP.

## CUBE e ROLLUP

### CUBE
A função CUBE permite gerar subtotais em várias dimensões, proporcionando uma visão mais abrangente dos dados.

### ROLLUP
Já a função ROLLUP simplifica a criação de subtotais, apresentando resultados agrupados de forma hierárquica.

## Exemplo de aplicação
Considere uma tabela de vendas. O código a seguir utiliza CUBE para calcular subtotais de vendas por produto e região:

```sql
SELECT produto, regiao, SUM(valor) as total_vendas
FROM tabela_vendas
GROUP BY CUBE (produto, regiao);
```

O resultado incluirá subtotais para cada produto, região e combinações dessas dimensões.

```sql
+---------+--------+--------------+
| produto | regiao | total_vendas |
+---------+--------+--------------+
| A       | Norte  | 100          |
| A       | Sul    | 200          |
| A       | NULL   | 300          |
| B       | Norte  | 150          |
| B       | Sul    | 120          |
| B       | NULL   | 270          |
| NULL    | Norte  | 250          |
| NULL    | Sul    | 320          |
| NULL    | NULL   | 570          |
+---------+--------+--------------+

```

Para ROLLUP, o código abaixo mostra como obter subtotais de vendas por região:

```sql
SELECT regiao, SUM(valor) as total_vendas
FROM tabela_vendas
GROUP BY ROLLUP (regiao);
```

O resultado incluirá subtotais acumulados para cada região.

```sql
+--------+--------------+
| regiao | total_vendas |
+--------+--------------+
| Norte  | 250          |
| Sul    | 320          |
| NULL   | 570          |
+--------+--------------+
```

## Conclusão
Compreender as funcionalidades CUBE e ROLLUP eleva a análise de dados no SQL. Ao explorar essas ferramentas, os usuários podem extrair insights mais profundos e valiosos de suas informações, e não ficar dependendo de ferramentas de BI para fazer essas análises mais simples de totalização e subtotais.

Este artigo foi gerado utilizando inteligência artificial generativa e passou por algumas revisões e edições antes de ser publicado. Para se conectar comigo, siga o meu LinkedIn: [Cayo Eduardo](https://www.linkedin.com/in/cayo-eduardo-da-silva-neves-b8b72018b/).

#BancoDeDados #SQL #CUBE #ROLLUP