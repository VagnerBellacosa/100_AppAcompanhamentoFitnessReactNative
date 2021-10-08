# React Native + Expo

## Parte do curso de React Native + Expo que apresentei aos meus colegas.

[![Roger Cruz](https://miro.medium.com/fit/c/28/28/2*rDqYKzAydYbYZzQ1AHPL0Q.jpeg)](https://rogercruz.medium.com/?source=post_page-----40e5574c6904-----------------------------------) [Roger Cruz](https://rogercruz.medium.com/?source=post_page-----40e5574c6904-----------------------------------) - [May 27, 2019·5 min read](https://rogercruz.medium.com/react-native-com-expo-um-exemplo-40e5574c6904?source=post_page-----40e5574c6904-----------------------------------)



E**xpo** é uma ferramenta utilizada no desenvolvimento mobile react-native. Permite fácil acesso às API’s desenvolvidas pelo expo.com. Não é preciso instalar qualquer dependência, transmutar ou configurar módulos de código nativo (java ou swift). Tudo acontece utilizando somente javascript.

> Utilizar Expo é um atalho para que o desenvolvedor front end comece a criar aplicativos mobile. Muito coisa pode ser feita com o seu conhecimento prévio em desenvolvimento de interfaces.

Pré Requisitos:

- n[ode.js](https://nodejs.org/en/download/)
- expo cli (terminal)

```
$ npm install expo-cli — global
```

- Criar uma conta de usuário expo:

![img](https://miro.medium.com/max/30/1*LWdQBkdOs9qJzIJcnza2Hg.png?q=20)

![img](https://miro.medium.com/max/700/1*LWdQBkdOs9qJzIJcnza2Hg.png)

Download do app [Android](https://play.google.com/store/apps/details?id=host.exp.exponent&referrer=www) ou [ios](https://itunes.apple.com/app/apple-store/id982107779) do Expo.

# Por que usar Expo ?

- Configuração zero
- Bibliotecas consolidadas já inclusas no SDK

Se você já desenvolveu usando a lib react, provavelmente conhece o set up “[Create React App](https://github.com/facebook/create-react-app)”. Expo é um set up similar para desenvolvimento react-native. Quando usamos expo cli para criar o aplicativo a plataforma gerencia o máximo possível da complexidade envolvida no processo.

> Essa forma de administração do processo de desenvolvimento é chamado de fluxo de trabalho gerenciado. Um desenvolvedor que usa o fluxo de trabalho gerenciado não precisa usar o Xcode ou o Android Studio, apenas desenvolve utilizando javaScript gerenciando a configuração por meio do [app.json](https://docs.expo.io/versions/latest/workflow/configuration/) presente na estrutura do "boilerplate" expo.

O fluxo de trabalho gerenciado ainda não está pronto para ser usado em todos os tipos de aplicativos. Há muitos casos em que as restrições atuais podem não ser apropriadas, como por exemplo quando precisamos incluir pedaços de código em swift.

![img](https://miro.medium.com/max/30/1*l2fuaIZ4b6v72kfub2N5hQ.png?q=20)

![img]()

**Fluxo de trabalho gerenciado(expo cli) vs react-native cli**

# Limitações

- Não é possível utilizar código Nativo em conjunto.
- O SDK não suporta todos os tipos de execução de código em segundo plano.
- Se você precisa manter o tamanho do seu aplicativo extremamente enxuto ( menor que 20mb )
- Se você deseja usar um serviço de notificação por push especifico que não o já incluso no expo.
- Se você deseja prover suporte para versões de código inferiores ao Android 5 e ao iOS

[Documentação](https://docs.expo.io/versions/v32.0.0/introduction/why-not-expo/)

# Primeiro Exemplo

Desenvolvimento de um app relógio.

Ao invés de desenvolver um aplicativo básico como o clássico hello word, optei por desenvolver um relógio (básico). Dessa maneira ficará um pouco mais didático entender a dinâmica e o ciclo de vida de uma aplicação react-native na prática.

# Passo 1

No terminal navegue até seu "workspace" e digite:

```
expo init clock
```

Algumas opções serão apresentadas, selecione as seguintes:

```
Choose a template: blank
Choose which workflow to use: managed
```

Após um output como esse:

```
Please enter a few initial configuration values.
 Read more: https://docs.expo.io/versions/latest/workflow/configuration · 100% completed
? Yarn v1.13.0 found. Use Yarn to install dependencies? Yes
[14:49:54] Extracting project files…
[14:49:55] Customizing project…
[14:49:55] Initialized a git repository.
[14:49:55] Installing dependencies…
```

# Passo 2

```
$ cd clock && yarn start
```

![img](https://miro.medium.com/max/30/1*BT07bKVeHCf-7JhxrZhcXA.png?q=20)

![img](https://miro.medium.com/max/700/1*BT07bKVeHCf-7JhxrZhcXA.png)

Agora o app está rodando. A informação do prompt é auto descritiva, existem algumas opções para visualizar o app:

- Fazer login no app do telefone com a conta criada
- Escanear o QR code com Expo app (android ) ou câmera iOS (atalho para o app expo)
- Rodar com emulador (é necessário instalar o Emulador) e pressionar i para iOS ou a para Android.

A facilidade de executar o código no dispositivo real acontece pois uma vez logado com sua conta expo no cli e no app a opção de abrir o app aparece listada no app expo automaticamente.

![img](https://miro.medium.com/max/30/1*FIr_4oXegoNIYdOsEy38Vw.png?q=20)

![img](https://miro.medium.com/max/700/1*FIr_4oXegoNIYdOsEy38Vw.png)

Optei por utilizar o simulador. O mesmo comportamento será obtido caso a opção de rodar no dispositivo real seja escolhida ([Documentação completa](https://docs.expo.io/versions/v32.0.0/workflow/up-and-running/)).

# Passo 3

Antes de começar de fato com o código. Algumas considerações precisam ser feitas.

A principal diferença entre código React (html) e react-native são os componentes nativos. A maioria dos aplicativos usará um desses componentes básicos. Você precisa se familiarizar com tudo isso antes de começar.

![img](https://miro.medium.com/max/30/1*Iwsyvvl98qeXAl4Jjnjbsg.png?q=20)

![img](https://miro.medium.com/max/700/1*Iwsyvvl98qeXAl4Jjnjbsg.png)

![img](https://miro.medium.com/max/30/1*XE_4DOxvDQPuN167AYtHfQ.png?q=20)

![img](https://miro.medium.com/max/700/1*XE_4DOxvDQPuN167AYtHfQ.png)

```
import React from ‘react’;
import { StyleSheet, Text, View } from ‘react-native’;export default class App extends React.Component {
 render() {
  return (
  <View style={styles.container}>
     <Text>Open up App.js to start working on your app!</Text>
  </View>
  );
 }
}const styles = StyleSheet.create({
 container: {
   flex: 1,
   backgroundColor: ‘#ffffff’,
   alignItems: ‘center’,
   justifyContent: ‘center’,
 },
});
```

Após iniciarmos, esse código no arquivo app.js.

O exemplo que proponho para entender o expo junto com o fluxo do react é o desenvolvimento de um relógio básico.

Nesse exemplo tempos o ciclo de vida básico de uma aplicação:

Segue abaixo uma breve definição dos métodos:

constructor(): Este método é usado para inicializar nosso componente com estado inicial, nenhum elemento de UI nativo foi renderizado ainda.

componentDidMount(): Este método também é invocado uma vez após a UI nativa para este componente terminar de renderizar, este é um bom lugar para fazer algum trabalho em dados, atualizar o estado, invocará o método render () novamente.

componentWillUnmount() : Este método é chamado quando o componente é removido, os usuários podem limpar os timers de execução, interromper as solicitações de rede e limpar qualquer valor armazenado anteriormente no aplicativo nesse método.

render(): Este método deve retornar um componente React Native (elemento JSX) para renderizar (ou nulo, para não renderizar nada).

Código:

```
import React from "react";
import { StyleSheet, Text, View, ScrollView, TextInput } from "react-native";export default class App extends React.Component {
  //Este método é usado para inicializar nosso componente com estado inicial, nenhum elemento de UI nativo foi renderizado
  constructor(props) {
    super(props);
    this.state = {
      date: new Date()
    };
  }tick() {
    this.setState({
      date: new Date()
    });
  } componentDidMount() {
     this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }  componentWillUnmount() {
      clearInterval(this.timerID);
  }render() {
    return (
        <View style={styles.container}>
          <Text style={styles.clock}>Clock</Text>
          <Text style={styles.clock}>     {this.state.date.toLocaleTimeString()}</Text>
        </View>
      )
  }
}const styles = StyleSheet.create({
  container: {
    flex: 1,
    flexDirection: 'column',
    alignItems: 'center',
    width: '100%',
    backgroundColor: 'black',
    marginTop: 50
  },
  clock: {
    fontSize: 50,
    color: '#bf740e',
    marginTop: 50
  }
});
```

![img](https://miro.medium.com/max/15/1*0C-UzZSzXosQmTFlXa8EHA.png?q=20)

![img](https://miro.medium.com/max/339/1*0C-UzZSzXosQmTFlXa8EHA.png)

Neste post procurei explorar a estrutura mínima de um projeto "single page". Nenhuma biblioteca do expo foi de fato utilizada. O que fiz foi aproveitar a ferramenta(expo) para facilitar os processos de build e teste,

Nos próximo posts pretendo mostrar algumas bibliotecas já integradas, que permitem fazer roteamento, navegação, obter geolocalização e executar audio/vídeo.

# Referências

- [https://docs.expo.i](https://docs.expo.io/versions/latest/workflow/up-and-running/)o
- https://facebook.github.io/react-native/

https://policy.medium.com/medium-terms-of-service-9db0094a1e0f?source=post_page-----40e5574c6904-----------------------------------)