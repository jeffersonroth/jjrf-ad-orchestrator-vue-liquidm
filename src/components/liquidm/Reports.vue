<template>
  <v-app
    id="Reports"
    dark>

    <v-layout>
        <v-form v-model="report">
            <v-container>
            <v-layout>
                <v-flex
                xs24
                md18
                >
                    <v-text-field
                        v-model.trim="query"
                        :rules="['Required']"
                        label="Query"
                        placeholder="Enter Report query..."
                        @keypress.native.enter="visualReports()"
                        required
                    ></v-text-field>
                    <v-btn block v-on:click="visualReports()" class="query" dark>Search</v-btn>
                </v-flex>

            </v-layout>
            </v-container>
        </v-form>

        <span class="loading" v-if="loading">Querying "{{ query }}"...</span>

        <div class="box" v-if="results && !loading || error && !loading">

            <div v-if="results" class="center">

                <p> {{results}} </p>
                
            </div>

            <span v-if="error">Error: "<i>{{ error }}</i>"!</span>

        </div>

    </v-layout>

  </v-app>
</template>

<script>
export default {
  name: 'reports',
  metaInfo () {
    return {
      title: 'LiquidM - Reports'
    }
  },
  data () {
    return {
        query: '',
        results: '',
        error: '',
        loading: false,
        option: 'reports',
    }
  },
  methods: {
      visualReports: report => {
          if ( this.query ) {
                this.loading = true;
                console.log('visualReports: ', this.query);
                var URL_REPORT = '/liquidm/reports';
                var METHOD_REPORT = 'GET';
                var REQ_PARAMS_REPORT = this.query;
                var BASE_URL_REPORT = 'https://platform.liquidm.com/visual_reports.json?auth_token=' + AUTH_TOKEN_LIQUIDM + '&' + REQ_PARAMS_REPORT;
                console.log('BASE_URL_REPORT: ' + BASE_URL_REPORT);
                var HEADERS_REPORT = {'cache-control': 'no-cache'};
                const getReport = async URL_REPORT => {
                    try {
                        const AXIOS_RESPONSE = await axios.get(BASE_URL_REPORT)
                        .then( AXIOS_RESPONSE => {
                            console.log('AXIOS_RESPONSE.status:', AXIOS_RESPONSE.status);
                            try {
                                this.results = AXIOS_RESPONSE.data;
                                this.error = '';
                                this.loading = false;
                                this.query = '';
                            } catch (error) {
                                console.log('Bad Request');
                                this.results = '';
                                this.error = error;
                                this.loading = false;
                                this.query = '';
                            }
                        });;
                    } catch (error) {
                        this.results = '';
                        this.error = error;
                        this.loading = false;
                        this.query = '';
                    };
                };
                getReport(URL_REPORT);
          } else {
                this.results = '';
                this.error = '';
                this.loading = false;
                this.query = '';
          }
      }
  },
  components: {
  }
}
</script>

<style>
</style>