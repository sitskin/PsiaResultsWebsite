<template>
 <div class="psia">
   <header>
    <div class="py-3 shadow mb-3 text-light">
        <div class="container">
            <img src="@/assets/PSIA.png">
            <h1 class="display-1">PSIA 2020 District 8AA Results</h1>
            <p class="lead">Building PSIA website template for future years.</p>
            <p>Light gray events do not have scores posted yet. Please check back later.</p>
        </div>
    </div>
  </header>
  <div class="events-lists">
    <div class="event-list" v-for="event in events">
      <div v-if="event.sections.length == 1">
        <div class="header" :class="event.sections[ 0 ].results ? 'clickable active' : ''" @click="event.display =  ! event.display"> {{ event.name }} -- {{ event.sections[ 0 ].grades }} </div>
        <!-- Single section event -->
        <table v-if="event.sections[ 0 ].results && event.display">
          <tr>
            <th> Place </th> <th> Name </th> <th> School </th> <th> State Qualifier</th>
          </tr>
          <tr class="result" v-for="result in event.sections[ 0 ].results">
            <td class="place"> {{ result.place }} </td>
            <td class="name"> {{ result.name }} </td>
            <td class="school"> {{ result.school }} </td>
            <td class="advances"> {{ result.advances ? "YES" : "" }} </td>
          </tr>
        </table>
      </div>
      <div v-else>
        <div class="header clickable active" @click="event.display = ! event.display"> {{ event.name }} </div>
        <!-- Muli section event -->
        <div v-for="section in event.sections">
          <div class="header" :class="section.results ? 'clickable active' : ''" v-if="event.display" @click="section.display = ! section.display"> {{ event.name }} -- {{ section.grades }} </div>
          <table v-if="section.results && section.display && event.display">
            <tr>
              <th> Place </th> <th> Name </th> <th> School </th> <th> State Qualifier</th>
            </tr>
            <tr class="result" v-for="result in event.sections[ 0 ].results">
              <td class="place"> {{ result.place }} </td>
              <td class="name"> {{ result.name }} </td>
              <td class="school"> {{ result.school }} </td>
              <td class="advances"> {{ result.advances ? "YES" : "" }} </td>
            </tr>
          </table>
        </div>
      </div>
    </div>
  </div>
 </div>
</template>

<script>
export default {
  name: 'psiaHome',
  data () {
    return {
      events: [
        {
          name: "Art Memory",
          display: false,
          sections: [
            {
              grades: "4,5",
              display: false,
              results: [
                { place: "1", name: "Genevieve Willett / 206", school: "Regents", advances: true },
                { place: "2", name: "George Melton / 96", school: "Hyde Park Schools", advances: true },
                { place: "3", name: "Jack McAdams / 73", school: "Regents", advances: false },
                { place: "4", name: "Mark Ayrault / 50", school: "Regents", advances: false },
              ],
            },
            {
              grades: "6-8",
              display: false,
              results: [
                { place: "1", name: "Emily Fletcher / 260", school: "St. Theresa", advances: true },
                { place: "2", name: "Mack Barley / 179", school: "Hyde Park Schools", advances: false },
                { place: "3", name: "Josephine Addison / 80", school: "St. Theresa", advances: false },
              ],
            },
          ],
        },
        {
          name: "Calculator Applications",
          display: false,
          sections: [
            {
              grades: "6-8",
              display: false,
              results: [
                { place: "1", name: "Emily Fletcher / 189", school: "St. Theresa", advances: true },
                { place: "2", name: "Stella Li / 124", school: "St. Theresa", advances: true },
                { place: "3", name: "Ryan Mcdonald / 111", school: "St. Theresa", advances: false },
                { place: "4", name: "Paul Berend / -43", school: "St. Louis", advances: false },
              ],
            },
          ],
        },
        {
          name: "Creative Writing",
          display: false,
          sections: [
            {
              grades: "1",
              display: false,
              results: undefined,
            },
            {
              grades: "2",
              display: false,
              results: undefined,
            },
          ],
        },
        // {
        //   name: "",
        //   sections: [
        //     {
        //       grades: "",
        //       results: undefined,
        //     },
        //   ],
        // },
      ],
    }
  },
  methods: {

  },
}
</script>

<style scoped lang="scss">
.clickable {
  cursor: pointer;
}
header {
	color: #FFF;
	background-color: #4c2079;
}
.events-lists {
  .event-list {
    .header {
      margin: 10px;
      color: grey;
      &.active {
        color: blue;
      }
    }
    table {
      min-width: 75%;
      margin-left: auto;
      margin-right: auto;
      border-collapse: collapse;
      border: 2px solid navy;
      tr {
        &:nth-child( odd ) {
          background-color: rgb(207, 226, 255);
        }
        &:nth-child( even ) {
          background-color: lightblue;
        }
      }
    }
    .results {
      .result {
        display: flex;
        flex-flow: row nowrap;
        justify-content: space-between;
      }
    }
  }
}
</style>
