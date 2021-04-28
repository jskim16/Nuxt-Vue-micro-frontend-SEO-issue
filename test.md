# Nuxt와 vue환경의 마이크로 프론트엔드에서의 SEO 작업

## nuxt에서의 SEO 적용 방법
[관련문서](https://nuxtjs.org/docs/2.x/configuration-glossary/configuration-mode)<br>
nuxt에서 SPA를 사용하는 경우 지원하는 모드 중에 CSR과 SSR을 지원하는 `universe` 모드가 있다. 그리고 CSR만 지원하는 `spa`모드도 있다. SEO를 하기 위해서는 CSR이 필요하기 때문에 `universal` 모드를 적용하는 방향으로 작업을 진행했다. 우선 모드의 동작을 확인하고 사용법을 익히기 위해 기본적인 Nuxt 프로젝트를 만들고 앱 내에서 모드별로 동작을 시켜보았다. 

```vue.js
//nuxt.config.js
export default {
  mode: 'universal',
  ssr: true,
  ...
}
  ```

nuxt로 프로젝트를 구동시켰을 때 spa모드로 구동했을 경우 페이지에 관한 렌더링이 소스 코드에 없었지만 universe모드로 구동했을 때 페이지 렌더링이 소스 코드에 올라온 것을 확인하였다.


## Nuxt를 이용한 마이크로 프론트엔드 환경 구현
이전 작업에서 vue를 이용한 마이크로 프론트엔드 구현은 [single-spa](https://github.com/single-spa/single-spa)를 이용해 구현하였다. Nuxt를 이용한 마이크로 프론트엔드는 single-spa를 기반으로 하는 [qiankun](https://qiankun.umijs.org/guide)을 기반으로 구현된 것을 분석했다. Nuxt에서 SSR 사용 가능 여부를 확인하기 위해 qiankun기반으로 구현된 [데모](https://github.com/FEMessage/nuxt-micro-frontend)를 사용하였다.

## nuxt 기반으로 한 마이크로 프로젝트에서의 SEO 적용
qiankun과 nuxt를 기반으로 한 마이크로 프론트엔드의 코드를 살펴보니 spa모드로 적용되어 있는 것을 확인하였다.
이를 universal 모드로 변경했을 때 동작을 확인하였다.
결과로는 window 오류가 발생하였고 node_module에 있는 파일에서 정보를 받지 못하는 에러가 발생하였다.

![window 오류](https://github.com/jskim16/Nuxt-micro-frontend/blob/main/img/window-is-not-defined.PNG)

결론적으로는 이 오류는 해결할 수 없다는 [답변](https://github.com/umijs/qiankun/issues/772)이 있었다.
## 정리
이 문제에 대한 똑같은 이슈제기가 있어 확인해보았다.
그에 대한 답변이 올라왔는데 마이크로 프론트엔드 구조가 qiankun기반을 하기 때문에 universal 모드는 사용이 불가능하다는 내용이었다.
현재 nuxt로 마이크로 프론트엔드 프로젝트를 만들려면 qiankun이 필요하기 때문에 nuxt에서 SEO 동작은 불가능하였다.
