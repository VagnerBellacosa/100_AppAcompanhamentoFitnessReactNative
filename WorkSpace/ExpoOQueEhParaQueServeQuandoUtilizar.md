# Expo: o que é, para que serve e quando utilizar?

O Expo é uma ferramenta utilizada no desenvolvimento mobile com React Native que permite o fácil acesso às API's nativas do dispositivo sem precisar instalar qualquer dependência ou alterar código nativo. Nesse post vamos falar sobre suas limitações e quando utilizar.

- [![Diego Fernandes](https://blog.rocketseat.com.br/content/images/size/w100/2019/05/profile.png)](https://blog.rocketseat.com.br/author/diego/)

#### [Diego Fernandes](https://blog.rocketseat.com.br/author/diego/)

27 de Mar de 2018 • 2 min read

![Expo: o que é, para que serve e quando utilizar?](https://blog.rocketseat.com.br/content/images/size/w2000/2018/12/expo-react-native.jpg)

O ***\*Expo\**** é uma ferramenta utilizada no desenvolvimento mobile com [***\*React Native\****](https://facebook.github.io/react-native/) que permite o fácil acesso às API’s nativas do dispositivo sem precisar instalar qualquer dependência ou alterar código nativo.

Apesar de cumprir esse papel muito bem, o Expo possui algumas desvantagens, principalmente para programadores que estão migrando de um estágio iniciante para intermediário com React Native e por isso vamos analisar todas ***\*vantagens do Expo\**** e pontos negativos nesse post.

Se você seguiu nosso [Minicurso de React Native para iniciantes](https://rocketseat.com.br/starter/curso-gratuito-react-native), provavelmente percebeu que não utilizei o Expo durante as aulas e nesse post vou explicar o motivo disso.

Caso ainda não tenha começado o ***\*desenvolvimento com React Native\****, recomendo muito ler [esse post](https://blog.rocketseat.com.br/3-passos-para-aprender-react-native/).

## Para que serve o expo?

Quando iniciamos no desenvolvimento mobile percebemos que o número de API’s e recursos nativos que podemos controlar através da nossa aplicação é gigante, e muitas vezes não nos recordamos de todas opções que temos disponíveis.

O Expo, por sua vez, oferece grande parte desses recursos de forma nativa e integrada e, por exemplo, você tem acesso à recursos como câmera, microfone, player de música, entre outros, de forma muito simples utilizando essa ferramenta.

Apesar de todos esses benefícios, o grande ponto do Expo para quem está iniciando é que para começar a desenvolver suas aplicações mobile com React Native você não precisará instalar a SDK do Android ou o XCode para Mac, isso porque o Expo possui um aplicativo móvel instalável pelas lojas do ***\*Android/iOS\**** que contém todo código nativo necessário pelo React Native para iniciar sua aplicação e, dessa forma, a única alteração em código que você faz é em ***\*Javascript\****.

O ponto destacado acima, na minha opinião, tem dois lados. A ***\*vantagem\**** é que nesse formato o desenvolvedor inicia muito rápido e em poucos minutos está criando sua aplicação, toda parte complicada foi abstraída. A ***\*desvantagem\**** está em exatamente pular essas etapas pois desconhecendo todo processo de instalação da SDK do Android ou XCode para iOS vai te limitar ***\*MUITO\**** futuramente para lidar com processos de atualização e build das aplicações.

## Quando utilizar?

Minha recomendação é que você utilize o Expo apenas em duas situações:

1. Você está testando o React Native e quer entender como ele funciona;
2. Você não tem interesse em publicar e manter aplicações mobile complexas (apenas criar apps simples).

“Ah, mas por que você não gosta do Expo?” Não é uma questão de não gostar, eu acredito que essa ferramenta tem seu espaço, mas, por experiência, ter todo conhecimento por volta do ecossistema ***\*Android\**** e ***\*iOS\**** para publicação e manutenção dos apps vai te dar muita flexibilidade enquanto que com o Expo você ficará totalmente restrito a utilizar as features conforme são lançadas.

## Concluindo

Apesar de extremamente fácil de configurar, na minha opinião, o Expo ainda não está maduro suficiente para ser utilizado em projetos maiores e que principalmente precisam ser mantidos constantemente. Suas vantagens para iniciantes são rapidamente perdidas conforme o conhecimento é maior e acabam se tornando pontos negativos para o desenvolvedor, o qual não terá conhecimento necessário na SDK do Android e iOS para realizar futuras modificações nessas plataformas.

A dor e os problemas de instalar o ambiente de desenvolvimento sem Expo no início valem a pena futuramente na hora de publicar e manter os apps.