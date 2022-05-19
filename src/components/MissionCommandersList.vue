<template>
  <div class="list row">
    <div class="col-md-6">
      <h4>Seccion de Mission Commanders</h4>
      <ul class="list-group">
        <li
          class="list-group-item"
          :class="{ active: index == currentIndex }"
          v-for="(commander, index) in commanders"
          :key="index"
          @click="setActiveCommander(commander, index)"
        >
          {{ commander.username }}
        </li>
      </ul>
    </div>
    <div class="col-md-6">
      <div v-if="currentCommander">
        <h4>Commander</h4>
        <div>
          <br /><label><strong>Nombre:</strong></label>
          {{ currentCommander.name }} <br /><label
            ><strong>Username:</strong></label
          >
          {{ currentCommander.username }} <br /><label
            ><strong>mainStack:</strong></label
          >
          {{ currentCommander.mainStack }} <br /><label
            ><strong>Current Enrollment:</strong></label
          >
          {{ currentCommander.currentEnrollment }} <br /><label
            ><strong>Has Azure Certification:</strong></label
          >
          {{ currentCommander.hasAzureCertification }}
        </div>

        <router-link
          :to="'/commander/' + currentCommander.id"
          class="btn btn-info"
        >
          Editar</router-link
        >
      </div>
      <div v-else>
        <br />
        <p>Selecciona un Mission Commmander.</p>
      </div>
    </div>
  </div>
</template>
<script>
import MissionCommanderService from "../services/MissionCommanderService";

export default {
  name: "commander-list",
  data() {
    return {
      tutorials: [],
      commanders: [],
      currentTutorial: null,
      currentCommander: null,
      currentIndex: -1,
      title: "",
      commanderId: "",
    };
  },
  methods: {
    getAllMissionCommanders() {
      MissionCommanderService.getAll()
        .then((response) => {
          this.commanders = response.data;
        })
        .catch((e) => {
          console.log(e);
        });
    },
    setActiveCommander(commander, index) {
      this.currentCommander = commander;
      this.currentIndex = commander ? index : -1;
    },
  },
  mounted() {
    this.getAllMissionCommanders();
  },
};
</script>
