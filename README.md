# vue_routing

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
