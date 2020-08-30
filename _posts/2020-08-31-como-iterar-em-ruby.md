---
layout: post
title:  "Como Iterar em Ruby?"
---

## Primeiras Impressões

Caso seja um iniciante na programação, estará muito acostumado com isso:

```c
for(int i = 0; i <= 10; i++) {
        printf("%d", i);
}
```

Caso seja um pouco mais ousado, provavelmente já terá encontrado isso:

```javascript
elements.forEach(function(e) {
  e.addClass('active');
});
```

Para quem conhece só a primeira forma de iterar, o choque com as iterações em Ruby será maior. Para quem já conhece a segunda forma (que existe em outras linguagens de forma semelhante, mas não idêntica) não será tão impactante.

Aqui está a forma mais simples de iterar em Ruby:

```ruby
users.each do |user|
  user.notify!
end
```

Essa forma, não é a mais elegante, porém é bastante encontrada. Existe outra forma menos elegante, que é esta:

```ruby
for i in 0..10
  puts i
end
```

Mesmo essa forma, que pelo menos encontramos a palavra `for` no meio, é bem diferente do que encontramos em outras linguagens. Minhas primeiras dúvidas quando vi essa iteração pela primeira vez foram:

- Como faço se eu não quero incrementar de um em um?
- Onde está a condição?
- Como que eu itero do maior para o menor?

Esta forma de iterar é deveras limitada, você não consegue tudo com ela, porém, a linguagem Ruby é poderosa, elegante, carismática e bela, você consegue implementar o que quer de uma forma ou de outra. No entretanto, o que eu percebi nos meus primeiros dias usando Ruby, é que geralmente não precisamos iterar de uma forma tão imperativa, na verdade, podemos alcançar o que queremos de outras formas.

## Oito tons de iteração

### for


```ruby
for i in 0..10
  puts i
end
```

### times

```ruby
2.times { "hello friend" }
```

```ruby
3.times { |index| puts index }
```

É nessa forma que as pessoas se apaixonam por Ruby, você está escrevendo um texto corrido praticamente. Quer executar alguma coisa quatro vezes? Ótimo, escreva `4.times { execute_your_beautiful_code }`.

### each

Muitas pessoas conhecem esta forma de outras linguagens, você tem alguns elementos dentro de uma coleção e você quer iterar sobre eles.

```ruby
students.each { |student| student.call_for_re_enrollment! }
```

### while

Aqui você está livre para fazer o que quiser. Também temos essa opção em outras linguagens.

```ruby
i = 0
while i < 10 do
  puts i
  i += 2 # pulando de dois em dois
end
```

Essa opção é um pouco mais verbosa comparada com as outras, mas tem seus usos.

Aqui está um exemplo mais real de como essa iteração pode ser usada.

```ruby
waiting_seconds = 0
while stack.deploying?
  logger.info("Waiting for deployment to complete")
  sleep waiting_seconds += 1
end
```

### until

Como disse, essa linguagem é linda. `until` é o contrário do `while`, ela executará enquanto a condição for `false`.

```ruby
until me.tired?
  me.work_hard
end
```

### loop

Se quiser ir para o infinito e além, use o `loop` para criar um _loop_ infinito.

```ruby
loop do
  # your code here..
  break if your_condition
end
```

### upto

Muito claro o que isso faz pelo nome, expõe lindamente o que queremos, ir de um índice até outro, existe uma variação dessa forma que será o próximo tópico.

```ruby
1.upto(10) { |i| puts index }
```

### downto

```ruby
10.downto(1) { |i| puts index }
```

## Usando Iterações como se Você Tivesse Nascido para Isso

### Enumerable

Leia a documentação do [Enumerable](https://ruby-doc.org/core-2.7.0/Enumerable.html). Veja os métodos que o módulo oferece, brinque com eles no terminal iterativo (IRB). É aqui que você elevará suas habilidades para se tornar o grande programador que o mundo quer conhecer. Com esse módulo você não somente ira iterar sobre listas, mas poderá transformá-las, reduzí-las, fazer perguntas, filtrar etc.

#### Iterando sobre uma fatia

```ruby
[1, 2, 3, 4, 5, 6].each_slice(3) { |slice| puts slice }
```

#### Transformando

```ruby
[1, 2, 3, 4].map { |number| { number.to_s => number ** 2 } }
```

#### Reduzindo

```ruby
[1, 2, 3, 4].reduce({ numbers: [] }) do |hash, number|
  hash[:numbers] << number
  hash
end
```

#### Questionando

```ruby
[2, 4, 6, 8, 10].all?(&:even?)
```

```ruby
[1, 4, 3, 8, 9].select(&:even?)
```

## Próximos passos

Essa pergunta no Stack Overflow para quem ficou com dúvidas sobre os últimos exemplos: [What does map(&:name) mean in Ruby?](https://stackoverflow.com/questions/1217088/what-does-mapname-mean-in-ruby).

Leia a documentação da classe `Array`, você encontrá vários métodos que você já viu no módulo `Enumerable`, porém encontrá muita coisa nova também: [`Array`](https://ruby-doc.org/core-2.7.0/Array.html).
