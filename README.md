# vue_routing

# 환경구축
# Vue Router 설치
# 1. 터미널에서 다음 명령어를 입력하여 Vue Router를 설치합니다.
     npm install vue-router

# 2. Vue Router 설정
# 설치 후 Vue Router를 설정해야 합니다.
     a. 라우터 파일 생성
     src 디렉토리 내에 router라는 폴더를 만들고 그 안에 index.js파일을 생성합니다. 이 파일에 라우터 설정을 작성합니다.

[code]

// src/router/index.js
import Vue from 'vue';
import Router from 'vue-router';
import Home from '../views/Home.vue'; // Home.vue를 임포트

Vue.use(Router);

const routes = [
  {
    path: '/',
    name: 'Home',
    component: Home,
  },
  // 다른 라우트 추가
];

const router = new Router({
  mode: 'history', // 해시 모드 대신 히스토리 모드 사용
  routes,
});

export default router;


[/code]

    b.라우터 추가
    main.js파일에서 라우터를 가져와 Vue인스턴스에 추가합니다.

[code]

// src/main.js
import Vue from 'vue';
import App from './App.vue';
import router from './router'; // 라우터 임포트

Vue.config.productionTip = false;

new Vue({
  router, // 라우터 추가
  render: h => h(App),
}).$mount('#app');

[/code]

# 3. 라우터 링크 사용
# 라우터를 설정한 후 내비게이션 링크를 추가하여 페이지 간 전환을 관리할 수 있습니다. 아래와 같이 NavigationBar.vue에서 라우터 링크를 사용할 수 있습니다.

[code]

<template>
  <nav class="bg-gray-100 p-4 rounded-md shadow-md" aria-label="breadcrumbs">
    <ul class="flex space-x-4">
      <li><router-link to="/" class="text-blue-600 hover:text-blue-800">Home</router-link></li>
      <li><router-link to="/about" class="text-blue-600 hover:text-blue-800">About</router-link></li>
      <li><router-link to="/services" class="text-blue-600 hover:text-blue-800">Services</router-link></li>
      <li><router-link to="/contact" class="text-blue-600 hover:text-blue-800">Contact</router-link></li>
      <li class="font-semibold text-gray-700">
        <router-link to="#" aria-current="page" class="text-gray-700">Current Page</router-link>
      </li>
    </ul>
  </nav>
</template>

[/code]

# 4. 페이지 컴포넌트 만들기
# 각 라우트에 대해 페이지 컴포넌트를 생성하세요. 예를 들어 Home.vue, About.vue, Services.vue, Contact.vue등을 생성하고 각각의 내용을 작성합니다.


===========<router/index.js>================

import Vue from "vue";
import VueRouter from "vue-router";
import MainHome from "@/components/MainHome";
import Corporate_Overview from "@/components/About_Us/Corporate_Overview";
import Company_Organization from "@/components/About_Us/Company_Organization";
import ProMise from "@/components/Introduction_Item/ProMise";
import GstaCAD from "@/components/Introduction_Item/GstaCAD";
import IronCAD from "@/components/Introduction_Item/IronCAD";
import Mech_Click from "@/components/Introduction_Item/Mech_Click";
import CompDelfoi from "@/components/Introduction_Item/CompDelfoi";
import CompLocation from "@/components/Customer_Support/CompLocation";
import Online_Inquiry from "@/components/Customer_Support/Online_Inquiry";
import Process_Simulator from "@/components/Equipment_Rental/Process_Simulator";
import Operation_Robot from "@/components/Equipment_Rental/Operation_Robot";
import VCOLP from "@/components/Introduction_Item/VCOLP";

Vue.use(VueRouter);

const router = new VueRouter({
  mode: "history",
  routes: [
    {
      path: "/",
      name: "home",
      component: MainHome,
    },
    {
      path: "/home",
      name: "Mainhome",
      component: MainHome,
    },
    {
      path: "/Corporate_Overview",
      name: "Corporate_Overview",
      component: Corporate_Overview,
    },
    {
      path: "/Company_Organization",
      name: "Company_Organization",
      component: Company_Organization,
    },
    {
      path: "/ProMise",
      name: "ProMise",
      component: ProMise,
    },
    {
      path: "/GstaCAD",
      name: "GstaCAD",
      component: GstaCAD,
    },
    {
      path: "/IronCAD",
      name: "IronCAD",
      component: IronCAD,
    },
    {
      path: "/Mech_Click",
      name: "Mech_Click",
      component: Mech_Click,
    },
    {
      path: "/CompDelfoi",
      name: "CompDelfoi",
      component: CompDelfoi,
    },
    {
      path: "/CompLocation",
      name: "CompLocation",
      component: CompLocation,
    },
    {
      path: "/Online_Inquiry",
      name: "Online_Inquiry",
      component: Online_Inquiry,
    },
    {
      path: "/Process_Simulator",
      name: "Process_Simulator",
      component: Process_Simulator,
    },
    {
      path: "/Operation_Robot",
      name: "Operation_Robot",
      component: Operation_Robot,
    },
    {
      path: "/VCOLP",
      name: "VCOLP",
      component: VCOLP,
    },
  ],
});

export default router;

===============<App.vue>===================

<template>
  <div id="app">
    <AppHeader
      :items="breadcrumbItems"
      :shouldShowBreadcrumb="shouldShowBreadcrumb"
      :navbarColor="navbarColor"
    />

    <router-view></router-view>
    <AppFooter />
  </div>
</template>

<script>
import AppHeader from "./components/AppHeader.vue";
import AppFooter from "./components/AppFooter.vue";

export default {
  name: "App",
  components: {
    AppHeader,
    AppFooter,
  },
  data() {
    return {
      breadcrumbItems: [],
      navbarColor: "#ea5519", // 기본 navbar 색상 설정
    };
  },
  watch: {
    $route: {
      immediate: true,
      handler(to) {
        this.updateBreadcrumb(to);
        this.updateNavbarColor(to); // navbar 색상 업데이트
      },
    },
  },
  computed: {
    // 현재 경로에 따라 바를 표시할지 여부를 결정하는 계산된 속성
    shouldShowBreadcrumb() {
      return this.$route.path !== "/" && this.$route.path !== "/Mainhome";
    },
  },
  methods: {
    updateBreadcrumb(route) {
      if (route.path === "/" || route.path.toLowerCase() === "/Mainhome") {
        this.breadcrumbItems = [];
      } else {
        this.breadcrumbItems = this.generateBreadcrumbItems(route);
      }
    },
    updateNavbarColor(route) {
      const path = route.path.toLowerCase(); // 경로를 소문자로 변환
      if (path === "/complocation" || path === "/online_inquiry") {
        this.navbarColor = "#384c74"; // 파란색
      } else {
        this.navbarColor = "#ea5519"; // 기본 색상으로 변경
      }
    },

    generateBreadcrumbItems(route) {
      const pathMap = {
        "/Corporate_Overview": ["회사소개", "사업개요"],
        "/Company_Organization": ["회사소개", "회사조직도"],
        "/CompDelfoi": ["제품소개", "SIMULATION"],
        "/GstaCAD": ["제품소개", "2D CAD"],
        "/IronCAD": ["제품소개", "3D CAD"],
        "/Mech_Click": ["제품소개", "LIBRARY"],
        "/ProMise": ["제품소개", "PMIS"],
        "/CompLocation": ["고객지원", "찾아오시는길"],
        "/Online_Inquiry": ["고객지원", "온라인문의"],
        "/Operation_Robot": ["장비임차", "ROBOT"],
        "/Process_Simulator": ["장비임차", "공정 시뮬레이터"],
        "/VCOLP": ["제품소개", "VCOLP"],
      };

      const breadcrumb = [];
      const pathArray = route.path.split("/").filter((p) => p);
      let currentPath = "";
      pathArray.forEach((segment) => {
        currentPath += `/${segment}`;
        if (pathMap[currentPath]) {
          pathMap[currentPath].forEach((item, index) => {
            breadcrumb.push({
              text: item,
              link: index < pathMap[currentPath].length - 1 ? currentPath : "",
            });
          });
        }
      });

      return breadcrumb;
    },
  },
};
</script>
