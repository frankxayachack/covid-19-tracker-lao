<template>
  <div class="container content">
    <section class="hero">
      <div class="hero-body">
        <div class="container has-text-centered">
          <h1 class="title">
            ຂໍ້ມູນການແພ່ລະບາດຂອງໂຣກຕິດເຊື້ອໄວຣັສໂຄໂຣນາສາຍພັນໃໝ່ 2019
          </h1>
          <p class="subtitle">
            ຂໍ້ມູນທາງສະຖິຕິຕໍ່ໄປນີ້ແມ່ນໄດ້ຮັບມາຈາກ API ຂອງທາງ
            <a
              href="https://github.com/NovelCOVID/API"
              target="_blank"
              rel="noopener noreferer"
              >github.com/NovelCOVID/API</a
            >
          </p>
          <p>
            ອັບເດດຂໍ້ມູນຫຼ້າສຸດເມື່ອວັນທີ
            {{
              laos.updated
                ? new Date(laos.updated)
                : new Date(laosAlt.updated) | moment("DD MMMM YYYY")
            }}
            ເວລາ
            {{
              laos.updated
                ? new Date(laos.updated)
                : new Date(laosAlt.updated) | moment("HH:mm:ss")
            }}
          </p>
        </div>
      </div>
    </section>
    <hr />
    <section class="columns">
      <div class="column">
        <SummaryCard
          type="is-warning"
          icon="virus"
          :overall="overall.cases"
          :laos="laos.cases || laosAlt.cases"
          >ກວດພົບ</SummaryCard
        >
      </div>
      <div class="column">
        <SummaryCard
          type="is-danger"
          icon="skull-crossbones"
          :overall="overall.deaths"
          :laos="laos.deaths || laosAlt.deaths"
          >ເສຍຊີວິດ</SummaryCard
        >
      </div>
      <div class="column">
        <SummaryCard
          type="is-success"
          icon="smile"
          :overall="overall.recovered"
          :laos="laos.recovered || laosAlt.recovered"
          >ຮັກສາແລ້ວ</SummaryCard
        >
      </div>
    </section>
    <hr />
    <b-table
      :data="allCountries"
      :columns="tableColumn"
      :default-sort="['cases', 'desc']"
      sticky-header
      height="100vh"
    ></b-table>
  </div>
</template>

<script>
// @ is an alias to /src
import SummaryCard from "@/components/SummaryCard";

export default {
  name: "Home",
  components: {
    SummaryCard
  },
  metaInfo: {
    title: "ໜ້າຫຼັກ",
    meta: [
      {
        vmid: "title",
        name: "title",
        content: "ໜ້າຫຼັກ - ເວັບໄຊຕິດຕາມການແພ່ລະບາດຂອງ COVID-19"
      },
      {
        vmid: "description",
        name: "description",
        content: "ເວັບໄຊຕິດຕາມການແພ່ລະບາດຂອງ COVID-19 ພາສາລາວແບບບໍ່ເປັນທາງການ"
      },
      {
        vmid: "og:type",
        name: "og:type",
        property: "og:type",
        content: "website"
      },
      {
        vmid: "og:title",
        name: "og:title",
        property: "og:title",
        content: "ໜ້າຫຼັກ - ເວັບໄຊຕິດຕາມການແພ່ລະບາດຂອງ COVID-19"
      },
      {
        vmid: "og:description",
        name: "og:description",
        property: "og:description",
        content: "ເວັບໄຊຕິດຕາມການແພ່ລະບາດຂອງ COVID-19 ພາສາລາວແບບບໍ່ເປັນທາງການ"
      },
      {
        vmid: "og:url",
        name: "og:url",
        property: "og:url",
        content: "https://covid19.artyboy.dev"
      },
      {
        vmid: "org:image",
        name: "org:image",
        property: "org:image",
        content: "https://covid19.artyboy.dev/covid19.webp"
      },
      {
        vmid: "twitter:card",
        name: "twitter:card",
        property: "twitter:card",
        content: "summary"
      },
      {
        vmid: "twitter:title",
        name: "twitter:title",
        property: "twitter:title",
        content: "ໜ້າຫຼັກ - ເວັບໄຊຕິດຕາມການແພ່ລະບາດຂອງ COVID-19"
      },
      {
        vmid: "twitter:description",
        name: "twitter:description",
        property: "twitter:description",
        content: "ເວັບໄຊຕິດຕາມການແພ່ລະບາດຂອງ COVID-19 ພາສາລາວແບບບໍ່ເປັນທາງການ"
      },
      {
        vmid: "twitter:url",
        name: "twitter:url",
        property: "twitter:url",
        content: "https://covid19.artyboy.dev"
      },
      {
        vmid: "twitter:image",
        name: "twitter:image",
        property: "twitter:image",
        content: "https://covid19.artyboy.dev/covid19.webp"
      }
    ]
  },
  data: () => {
    return {
      allCountries: [],
      laos: [],
      laosAlt: [],
      overall: [],
      tableColumn: [
        {
          field: "country",
          label: "ປະເທດ",
          sortable: true,
          width: 250,
          searchable: true
        },
        {
          field: "cases",
          label: "ກວດພົບ",
          sortable: true
        },
        {
          field: "todayCases",
          label: "ກວດພົບຫຼ້າສຸດ",
          sortable: true
        },
        {
          field: "deaths",
          label: "ເສຍຊີວິດ",
          sortable: true
        },
        {
          field: "todayDeaths",
          label: "ເສຍຊີວິດຫຼ້າສຸດ",
          sortable: true
        },
        {
          field: "recovered",
          label: "ຮັກສາແລ້ວ",
          sortable: true
        },
        {
          field: "active",
          label: "ກໍາລັງຮັກສາ",
          sortable: true
        },
        {
          field: "critical",
          label: "ອາການໜັກ",
          sortable: true
        }
      ]
    };
  },
  created: function() {
    this.getAllCountriesData();
    this.getLaosData();
    this.getLaosAltData();
    this.getOverallData();
  },
  methods: {
    getAllCountriesData() {
      this.$http
        .get("https://corona.lmao.ninja/v2/countries")
        .then(res => {
          this.allCountries = res.data;
        })
        .catch(err => {
          console.log(err);
          this.$buefy.toast.open({
            duration: 5000,
            message: `ບໍ່ສາມາດໂຫຼດຂໍ້ມູນແຕ່ລະປະເທດໄດ້, ກະລຸນາລອງໃໝ່ໃນພາຍຫຼັງ`,
            type: "is-danger",
            position: "is-bottom"
          });
        });
    },
    getLaosData() {
      this.$http
        .get("https://corona.lmao.ninja/v2/countries/lao")
        .then(res => {
          this.laos = res.data;
        })
        .catch(err => {
          console.log(err);
          this.$buefy.toast.open({
            duration: 5000,
            message: `ບໍ່ສາມາດໂຫຼດຂໍ້ມູນປະເທດລາວໄດ້, ກະລຸນາລອງໃໝ່ໃນພາຍຫຼັງ`,
            type: "is-danger",
            position: "is-bottom"
          });
        });
    },
    getLaosAltData() {
      this.$http
        .get("https://corona.lmao.ninja/v2/countries")
        .then(res => {
          let data = res.data;
          this.laosAlt = data.find(i => i.countryInfo.iso3 == "LAO");
        })
        .catch(err => {
          console.log(err);
          this.$buefy.toast.open({
            duration: 5000,
            message: `ບໍ່ສາມາດໂຫຼດຂໍ້ມູນປະເທດລາວໄດ້, ກະລຸນາລອງໃໝ່ໃນພາຍຫຼັງ`,
            type: "is-danger",
            position: "is-bottom"
          });
        });
    },
    getOverallData() {
      this.$http
        .get("https://corona.lmao.ninja/v2/all")
        .then(res => {
          this.overall = res.data;
        })
        .catch(err => {
          console.log(err);
          this.$buefy.toast.open({
            duration: 5000,
            message: `ບໍ່ສາມາດໂຫຼດຂໍ້ມູນພາບລວມໄດ້, ກະລຸນາລອງໃໝ່ໃນພາຍຫຼັງ`,
            type: "is-danger",
            position: "is-bottom"
          });
        });
    }
  }
};
</script>
