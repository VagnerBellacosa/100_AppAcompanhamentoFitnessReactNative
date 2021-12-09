# Otimize o desempenho do seu aplicativo React Native

#### Published by [**WP Info**](https://br.atsit.in/archives/author/wp-info-staff-team) on April 16, 2021



Uma ótima experiência do usuário deve ser o objetivo principal de qualquer desenvolvimento de aplicativo. Embora o [React Native ](https://reactnative.dev/)tente fornecer tudo que você precisa para desenvolver um aplicativo de alto desempenho, há ocasiões em que você para otimizar manualmente seu aplicativo. Para fazer isso, os desenvolvedores precisam ter uma mentalidade de otimização de desempenho desde o início de seus projetos.

A maioria dos dispositivos móveis modernos exibe 60 quadros em um segundo-o que significa [você tem 16,67 milissegundos para exibir um frame ](https://reactnative.dev/docs/performance)para que o aplicativo tenha um bom desempenho. Qualquer coisa abaixo disso resultará em baixo desempenho, e a IU pode até parecer que não está respondendo.

## Como o React Native funciona?

Um aplicativo React Native é composto de duas partes: os códigos JavaScript e os códigos nativos. Esses dois são completamente diferentes e normalmente não podem se comunicar uns com os outros por conta própria.

Eles só podem fazer isso por meio da Ponte Nativa React (também conhecida como Árvore da Sombra). A ponte fica entre os códigos JavaScript e os códigos nativos e envia objetos JSON serializados do encadeamento JavaScript para o encadeamento nativo e vice-versa.

Embora [o Facebook esteja trabalhando em uma arquitetura React Native aprimorada ](https://engineering.fb.com/2019/07/12/android/hermes/)(e [um motivo pelo qual você não deveria desistir do React Native ](https://blog.logrocket.com/why-keep-faith-react-native/)) que permitiria que os códigos JavaScript falassem diretamente com os códigos nativos por meio da Interface JavaScript (JSI), problemas de desempenho podem ocorrer facilmente na arquitetura atual ao lidar com processos complexos e grandes. É por isso que é importante otimizar seu aplicativo React Native antes de enviá-lo para produção.



Vejamos algumas das práticas recomendadas para melhorar o desempenho de um aplicativo React Native com vários exemplos de código.

## Use `FlatList `ou `SectionList `para renderizar listas grandes no React Native

Se você tiver uma lista grande, renderizar todos os itens de uma vez pode causar um problema de desempenho, mas o carregamento lento com `FlatList `pode melhorar o desempenho. O componente `FlatList `renderiza apenas os itens que serão exibidos na tela e os remove quando não são mais exibidos. Isso economiza muita memória, tornando o aplicativo muito mais rápido.

```
 import React from'react'
importar {FlatList} de'react-native' dados const=[ { id: 1, texto:'Primeiro' }, { id: 2, texto:'Second' }, ...
] const App=()=> { const renderItem=({item})=> (   {item.text}   ) Retorna (  item.id} /> )
}
```

`FlatList `e `SectionList `servem a propósitos semelhantes. Ambos podem melhorar o desempenho do seu aplicativo. No entanto, `SectionList `é mais adequado ao renderizar seções. `VirtualizedList `também pode ser usado se você precisar de mais flexibilidade.

Também é possível renderizar listas com `ListView `e, embora possa ser usado para listas pequenas, não é recomendado para listas grandes. Embora seja possível renderizar listas com `map `, não é aconselhável fazê-lo no React Native.

## Remova todas as instruções do console

As instruções do console são necessárias para depurar códigos JavaScript, mas destinam-se apenas a fins de desenvolvimento. Essas declarações podem causar sérios problemas de desempenho em seu aplicativo React Native se não forem removidas antes do empacotamento.

Embora você possa instalar alguns plug-ins como `babel-plugin-transform-remove-console `para remover essas instruções da produção, é melhor removê-los manualmente se não quiser adicionar mais dependências para seu aplicativo.

## Memorize cálculos caros

O React introduziu o `memo `HOC (Higher Order Component) no React 16.6 para evitar uma nova renderização desnecessária e o gancho `useMemo `no React 16.8 para otimizar cálculos caros.

No entanto, também é possível usar o gancho `useCallback `para fazer isso. A principal diferença entre `useMemo `e `useCallback `é que `useMemo `retorna um valor memorizado, mas `useCallback `retorna um retorno de chamada memorizado.

Vamos dar uma olhada em cada um deles.

### O `React.memo `Componente de Ordem Superior (HOC)

`React.memo `foi apresentado aos componentes funcionais para servir ao mesmo propósito que o `React PureComponents `serve em componentes de classe. `memo `evita uma nova renderização desnecessária de um componente e pode ajudar a otimizar um aplicativo.



No entanto, como outras técnicas de otimização, `memo `só deve ser usado quando for necessário. Em alguns casos, a nova renderização desnecessária não afetaria tanto o desempenho.

Aqui está um exemplo para ilustrar o `memo `.

```
 import React from'react'
import {View, Text, TouchableOpacity} de'react-native' Elemento const=({filhos, valor, setValue})=> { const handleOperation=()=> setValue (valor * 2) Retorna (   {value}   {crianças}   ) } exportar elemento padrão 
 import React, {useState} de'react'
importar {View} de'react-native'
importar Elemento de'./Element' const App=()=> { const [firstNum, setFirstNum]=useState (5) const [secondNum, setSecondNum]=useState (5) Retorna(   Adicionar primeiro   Adicionar segundo   )
}
```

O problema com o código acima é que quando qualquer um dos botões é pressionado, ambos os botões são renderizados novamente, embora apenas os estados do botão pressionado sejam alterados.

Isso pode ser corrigido envolvendo o componente `Elemento `com o HOC `React.memo `. Veja como fazer isso.

```
 import React, {memo} de'react'
import {View, Text, TouchableOpacity} de'react-native' Elemento const=({filhos, valor, setValue})=> { const handleOperation=()=> setValue (valor * 2) Retorna (   {value}   {crianças}   ) } exportar memorando padrão (Elemento)
```

Isso resolveria o problema de renderização novamente. No entanto, deve ser usado apenas quando a nova renderização está causando alguns problemas de desempenho.

### O gancho `useMemo`

`useMemo `retorna um valor memorizado de uma função. No entanto, deve ser usado apenas ao realizar cálculos caros.

Por exemplo, suponha que desejamos filtrar alguns dados provenientes de nossa API por sua classificação. Poderíamos memorizar o cálculo para recalcular os resultados apenas quando os valores mudassem.

```
 const data=[ {id: 1, estado:'Texas', classificação: 4,5}, {id: 2, estado:'Havaí', avaliação: 3}, {id: 3, estado:'Illinois', classificação: 4}, {id: 4, estado:'Texas', avaliação: 5}, {id: 5, estado:'Ohio', classificação: 4,5}, {id: 6, estado:'Louisiana', classificação: 3}, {id: 7, estado:'Texas', avaliação: 2}, ... {id: 1000, estado:'Illinois', classificação: 4,5},
]
```

Se desejarmos filtrar os dados com base na classificação (sem memoização), podemos usar muita memória. Para tal, não queremos recalcular desnecessariamente os valores quando outros componentes forem renderizados novamente. Queremos renderizar novamente ou recalcular apenas quando a classificação dependente mudar.

Vamos ver como podemos fazer isso com `useMemo `.

```
 import React, {useMemo} de'react'
importar {FlatList} de'react-native'
importar dados de'./data' const App=()=> { const rateCompare=3; const computedValue=useMemo (()=> { //cálculo supostamente intensivo em computação resultado const=data.filter ((d)=> d.rating> rateCompare); resultado de retorno; }, [rateCompare]); const renderItem=({item})=> (   {item.state}   ); Retorna (  item.id} /> )
}
```

Presumimos que temos muitos dados provenientes de nossa API e precisamos realizar um cálculo intensivo de computação. Embora tenhamos usado uma operação de filtro simples, poderíamos estar fazendo uma série de cálculos aqui. Este é um bom caso de uso para o gancho `useMemo `.



Usando `useMemo `, podemos armazenar em cache (memorizar) os resultados para o valor especificado na matriz de dependência. Por exemplo, se a constante `rateCompare `era `3 `na primeira vez em que é executada, a função não recalculará sempre que o valor de `rateCompare `for `3 `mesmo se todos os componentes forem renderizados novamente. Ele só vai recalcular quando o valor mudar.

### O gancho `useCallback`

O gancho `useCallback `é semelhante a `useMemo `, mas retorna um retorno de chamada memorizado.

```
 import React, {useState, useEffect, useCallback} de'react'
importar {FlatList} de'react-native'
importar dados de'./data' const App=()=> { const [valores, setValues]=useState ([]); const rateCompare=3; const valuesCallback=useCallback (()=> { //cálculo supostamente intensivo em computação resultado const=data.filter ((d)=> d.rating> rateCompare); setValues (resultado); }, [rateCompare, setValues]); useEffect (()=> { valuesCallback (); }, [valuesCallback]); const renderItem=({item})=> (   {item.state}   ); Retorna (  item.id} /> )
}
```

Isso faz a mesma coisa que o exemplo `useMemo `. No entanto, como `useCallback `retorna uma função, precisamos chamar essa função para obter o valor. Aqui, chamamos a função em um gancho `useEffect `e, em seguida, renderizamos os valores em um componente `FlatList `.

Poderíamos igualmente ter chamado a função em um componente `Botão `ou `TouchableOpacity `. Dessa forma, o cálculo será executado sempre que o botão for pressionado.

```
 Button onPress={valuesCallback} title="Botão de exemplo"/>
```

Enquanto `React.memo `pode otimizar um componente inteiro, `useMemo `e `useCallback `podem otimizar um cálculo ou processo. No entanto, cada um deles deve ser usado apenas quando necessário, caso contrário, eles podem até agravar o problema de desempenho.

Recomenda-se escrever primeiro o cálculo ou componente sem memorização e apenas otimizá-lo (memorizá-lo) se estiver causando problemas de desempenho.

## Ajustar (redimensionar e diminuir) os tamanhos das imagens

As imagens podem contribuir significativamente para problemas de desempenho em aplicativos React Native. Eles também podem representar alguns problemas em aplicativos da web, mas o navegador tem a capacidade de baixar e até mesmo dimensionar as imagens. Em alguns casos, pode até armazená-los em cache.

Mas isso é diferente com os aplicativos para celular. O React Native vem com um componente `Image `que pode lidar muito bem com uma única imagem, mas funciona mal com muitas imagens de tamanho grande.

A melhor maneira de resolver este problema é carregando o tamanho exato da imagem que você precisa. Em outras palavras, você deve redimensionar e diminuir o tamanho da imagem antes de carregá-la em seu aplicativo.

## Armazenar imagens em cache localmente

O cache é outra solução para problemas de imagem em um aplicativo React Native. Ele salva as imagens localmente na primeira vez que são carregadas e usa o cache local nas solicitações subsequentes. Isso pode melhorar o desempenho do aplicativo notavelmente. Mas o armazenamento em cache com o componente de imagem é compatível apenas com iOS, não com Android.



Veja como você armazenaria uma imagem em cache.

```

```

No entanto, este método de armazenamento em cache não é o ideal porque dificilmente resolve os problemas. Vários problemas, como oscilação, perda de cache, desempenho insatisfatório do aplicativo e carregamento de desempenho insatisfatório do cache podem ocorrer quando a imagem é armazenada em cache dessa maneira. É possível resolver esse problema com a `react-native-fast-image `.

Além de armazenar imagens em cache, [Imagem Rápida ](https://github.com/DylanVann/react-native-fast-image)também adiciona cabeçalhos de autorização e vários outros recursos.

```
 importar FastImage de'react-native-fast-image' const App=()=> ( 
)
```

Você também pode usar algumas outras bibliotecas, como `react-native-cached-image `para armazenar em cache e carregar imagens. Veja como usá-lo.

```
 importar {CachedImage} de'react-native-cached-image'; 
```

## Use formatos de imagem de carregamento rápido no React Native

Junto com o tamanho da imagem, o formato da imagem também pode afetar o desempenho do aplicativo. Os desenvolvedores vindos do plano de fundo da web preferem os formatos `JPEG `e `JPG `porque eles permitem a compactação. No entanto, isso não é verdade para plataformas móveis.

Por outro lado, você pode reduzir o número de cores exclusivas em cada linha de pixels que compõem uma imagem `PNG `. Isso pode reduzir significativamente o tamanho da imagem. É suficiente dizer que o formato `PNG `é melhor do que o formato `JPG `para plataformas móveis.

O formato `WebP `introduzido pelo Google em 2010 é o de melhor desempenho dos três. [Suporta modos de compressão sem e com perda ](https://developer.android.com/topic/performance/network-xfer)e pode reduzir o tamanho da imagem em até 25-34%. Lembre-se de que este formato não é compatível com todos os dispositivos móveis. É compatível com dispositivos Android 4.2.1 e superior e iOS 14.

## Programe animações com `InteractionManager `e `LayoutAnimation`

Se não forem feitas corretamente, as animações podem afetar o desempenho de seu aplicativo React Native. O método `runAfterInteractions `de `InteractionManager `pode ser usado para agendar operações síncronas de longa duração após a conclusão de uma animação ou interação. Isso pode melhorar o desempenho de um aplicativo React Native, garantindo que as animações sejam executadas sem problemas.

```
 InteractionManager.runAfterInteractions (()=> { ...
});
```

Se você estiver preocupado com a experiência do usuário, pode ser preferível usar `LayoutAnimation `. Isso executaria a animação durante o próximo layout.

```
 import React, {useState} de"react";
importar {LayoutAnimation} de"react-native"; if (Platform.OS==='android'&& UIManager.setLayoutAnimationEnabledExperimental) { UIManager.setLayoutAnimationEnabledExperimental (true);
} const App=()=> { const [animate, setAnimate]=useState (false) const handleClick=()=> { LayoutAnimation.configureNext (LayoutAnimation.Presets.spring) setAnimate (! animate) } Retorna ( Button onPress={handleClick} title="Animar"/> )
}
```

O sinalizador `UIManager.setLayoutAnimationEnabledExperimental (true); `deve ser definido para garantir que funciona no Android.

## Use driver nativo com a API Animated

Executar uma animação no thread de JavaScript é uma má ideia. O encadeamento JS pode ser facilmente bloqueado e isso pode fazer a animação funcionar lentamente ou nem funcionar.

Porque a [API animada é serializável, é possível empurrar os detalhes da animação para nativos antes que a animação comece ](https://reactnative.dev/blog/2017/02/14/using-native-driver-for-animated). Como tal, os códigos nativos executarão a animação no thread de interface do usuário. Isso garantirá que a animação seja executada sem problemas, mesmo se o thread de JavaScript estiver bloqueado.

Veja como definir `useNativeDriver `com a API Animated.

```
 import React, {useRef} de'react'
importar {Animated} de'react-native' const App=()=> { const opacity=useRef (new Animated.value (0)). current const showVal=()=> { Animated.timing (opacidade, { toValue: 1, duração: 500, useNativeDriver: true, }).começar(); } ... Retorna (    Texto para mostrar   ) }
```

Aqui, declaramos uma variável `opacity `para conter o valor de opacidade. Definimos o valor inicial para `0 `e então usamos `Animated.timing `para acionar a animação no clique do botão. `useNativeDriver `é definido como `true `em `Animated.timing `para enviar detalhes da animação para Native.

## Remova bibliotecas e recursos desnecessários

Cada biblioteca em um aplicativo React ou React Native deixa alguma pegada no aplicativo. É por isso que você só deve adicionar bibliotecas e recursos de que precisa em seu aplicativo e remover dependências e bibliotecas irrelevantes. Animações, navegações, guias e outros recursos podem contribuir para o tempo de carregamento da tela e, portanto, quanto mais eles estiverem na tela, pior será o desempenho.

## Use Hermes

[Hermes ](https://reactnative.dev/docs/hermes)é um mecanismo JavaScript desenvolvido pelo Facebook em 2019. É um dos os recursos essenciais para melhorar o desempenho do aplicativo, reduzir o uso de memória, diminuir o tamanho do aplicativo e melhorar o tempo de inicialização do aplicativo.

O Hermes não está habilitado por padrão no React Native, mas você pode habilitá-lo facilmente no seu aplicativo.



Antes do lançamento do React Native 0.64, o Hermes estava disponível apenas para plataformas Android, mas com o lançamento recente, agora está disponível para iOS também.

Se estiver usando uma versão anterior do React Native, você precisa primeiro atualizá-lo para a versão aceitável antes de ativar o Hermes.

Para ativar o Hermes no Android, edite seu arquivo `android/app/build.gradle `e adicione as seguintes regras.

```
 project.ext.react=[ entryFile:"index.js", enableHermes: true ]
```

Você também pode fazer assim:

```
 def enableHermes=project.ext.react.get ("enableHermes", true);
```

Se você estiver usando o ProGuard, abra seu `proguard-rules.pro `e adicione as seguintes regras.

```
-manter classe com.facebook.hermes.unicode. ** {*; }
-manter a classe com.facebook.jni. ** {*; }
```

Em seguida, limpe e reconstrua seu aplicativo se você já o tiver feito. Para fazer isso, primeiro execute `cd android `e, em seguida, `./gradlew clean `.

Se você estiver atualizando sua versão do React Native, certifique-se de editar o arquivo `build.gradle `de acordo com o [Versões do Gradle ](https://gradle.org/releases/).

Curiosamente, Hermes para iOS foi lançado recentemente na nova versão React Native 0.64 em 12 de março de 2021. Para habilitar Hermes para iOS, defina `hermes_enabled `como `true `e execute `pod install `em seu `Podfile `.

```
 use_react_native! ( : path=> config [: reactNativePath], : hermes_enabled=> true
)
```

## Use `Selecionar novamente `com Redux

Como o gancho `useMemo `, `Reselect `pode ser usado para criar seletores memoized para otimizar cálculos caros. No entanto, ao contrário de `useMemo `, ele deve ser usado com `Redux `.

Assumindo que temos um estado `getPosts `de nossa loja Redux, podemos usar `Reselect `para selecionar as postagens com o maior número de curtidas e usuários nas postagens.



`Reselect `vem com a função `createSelector `que pode ser usada para criar seletores memoized, como mostrado abaixo.

```
 import {createSelector} de"reselect"
importar _ de"lodash" //seletor não memorizado
export const getAllPosts=(state)=> state.allPosts //seletor memorizado para obter postagens com as principais curtidas
export const getMostLiked=(likes)=> createSelector ( getAllPost, item=> item && _.filter (item, (post)=> post.likes>=likes)
) //seletor memorizado para obter os usuários com as melhores curtidas
export const getTopUsersByLikedPosts=(likes)=> createSelector ( getMostLiked (likes), item=> item && _ (item).map ((post)=> post.user).uniqBy (post=> post.id).value ()
)
```

Primeiro, criamos um seletor **não otimizado** `getAllPosts `de nosso estado redux `allPosts `. Em seguida, criamos um seletor **otimizado** `getMostLiked `em `getAllPosts `e, em seguida, filtramos os itens com base em seus gostos. Isso memoriza `getMostLiked `de modo que os valores serão recalculados apenas quando os dados de postagem forem alterados.

Além disso, criamos um seletor memoized, `getTopUsersByLikedPosts `, de `getMostLiked `e selecionamos os usuários das postagens. Isso garante que `getTopUsersByLikedPosts `mude apenas quando os principais gostos dos dados de postagens mudarem.

Este é apenas um exemplo. Poderíamos realizar qualquer cálculo caro aqui e memorizá-lo com `Selecionar novamente `.

`Selecionar novamente `deve ser usado apenas quando for necessário; o uso excessivo pode até agravar o problema de desempenho em seu aplicativo React Native.

## Monitore o uso de memória no React Native

Alguns processos e recursos podem usar uma quantidade incomum de memória do que você espera. A menos que você queira esses processos, desativá-los ou otimizá-los pode ser a chave para melhorar o desempenho de seu aplicativo React Native.

Você pode monitorar o uso de memória no Android Studio e [Xcode ](https://developer.apple.com/documentation/xcode/improving_your_app_s_performance)para encontrar vazamentos que podem estar afetando o desempenho do seu aplicativo.

Isso pode ser feito por meio do Memory Profiler no Android Studio. Você pode abrir o Memory Profiler em **Exibir> Janelas de ferramentas> Profiler** ou localizar o ícone **Perfil** na barra de ferramentas.

Você também pode monitorar o desempenho de seu aplicativo a partir do menu do desenvolvedor em seu aplicativo. Para abrir o menu do desenvolvedor, use o atalho **Command + M** (Mac) ou **Control + M** (Windows e Linux). No menu do desenvolvedor, alterne `Show Perf Monitor `para monitorar o desempenho de cada componente em seu aplicativo.

O Xcode também permite que os desenvolvedores encontrem oscilações ou vazamentos de memória em seus aplicativos. Você pode encontrar isso em **Produto> Perfil** . Como alternativa, você pode usar o atalho **Command + i** para abrir o Leaks Profiler. Reinicie seu aplicativo em seu simulador para começar a identificar os vazamentos de memória.

Vazamentos de memória podem ser causados por vários fatores, conforme discutido acima. Às vezes, as imagens em cache podem obstruir a memória e causar problemas. Em alguns casos, você pode simplesmente precisar alterar `ListView `para `FlatList `para corrigir o problema. Em qualquer caso, o Profiler mostrará a verdadeira causa do problema.

## Conclusão

O desempenho é um fator crucial em todos os aplicativos React Native, mas também é um tópico complexo.

Vários fatores podem afetar o desempenho, desde instruções e animações do console até imagens de grande porte e cálculos pesados. É importante identificar as fontes desses vazamentos de memória e baixo desempenho e corrigi-los.

Curiosamente, o Android Studio e o Xcode nos fornecem uma maneira de monitorar o uso de memória. Também temos uma infinidade de ferramentas e métodos para otimizar o desempenho dos aplicativos React Native, conforme discutido. Você pode experimentar essas técnicas de otimização em seu próximo projeto React Native.

A postagem [Otimize o desempenho do aplicativo React Native ](https://blog.logrocket.com/optimize-your-react-native-app-performance/)apareceu primeiro no [LogRocket Blog ](https://blog.logrocket.com/).

[Source link](https://blog.logrocket.com/optimize-your-react-native-app-performance/)