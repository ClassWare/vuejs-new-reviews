<template>
  <div class="hello">
    <h1>{{ msgParm }}</h1>
    <p>
      Please enter search criteria
    </p>

    <div class="container">
        <form>
          <div class="form-group form-group-sm">
            <label for="movieTitle">Title</label>
            <input type="text" class="form-control" id="movieTitle" v-model="movieTitle" v-on:change="filterData()">
            <label for="headLine">Headline</label>
            <input type="text" class="form-control" id="headLine" v-model="headLine" v-on:change="filterData()">
            <div class="checkbox">
              <label>
                <input type="checkbox" v-on:change="filterData()" > Critics Pick?</label>
            </div>
          </div>

          <button type="submit" class="btn btn-primary" @click.prevent="mySubmit">Submit</button>

        </form>
        <h3>Reviews</h3>
        <p v-if="loading">
          Loading
        </p>
        <div v-else>
          <!-- Try outlet here -->
          <router-view class="reviewDetails" name="reviewDetails"></router-view>

          <table class="table table-hover">
            <thead>
              <tr>
                <th>Action</th>
                <th>Entry</th>
                <th>Pick</th>
                <th>Title</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="review in outReviews" @click="reviewClicked(review)">
                <!-- <router-link to="/review" tag="tr" active-class="active"> -->
                <router-link :to="{name:'reviewDetails', params:{bla:'zog'} }" tag="td" active-class="active">
                    <a>X</a>
                </router-link>
                <td>{{ review.id }}</td>
                <td><input type="checkbox" v-bind:checked="review.pick"></td>
                <td>{{ review.title }}</td>
              </tr>
            </tbody>
          </table>
        </div>

    </div>

  </div>
</template>

<script>
export default {
  name: 'ReviewSearch',
  props: {
    msgParm: String
  },
  data() {
    return {
      movieTitle: "",
      headLine: "",
      loading: true,
      inReviews: [],
      outReviews: []
    }
  },
  mounted() {
    this.loadData()
  },
  methods: {
    mySubmit() {
      console.log("NOT Submitted");
    },
    reviewClicked(review) {
      console.log("REVIEW-CLICK " + review.id);
    },
    loadData() {
      var url='https://jsonplaceholder.typicode.com/posts';
      axios.get(url).then((response) => {
        this.inReviews = response.data;
        this.inReviews.forEach(function(obj, inx) {
          if (inx % 2) { obj.pick = false; }
          else { obj.pick = true; }
        });
        this.outReviews = this.inReviews;
        this.loading = false;
      });
    },
    filterData() {
      // console.log("Title: " + this.movieTitle);
      // console.log("Headline: " + this.headLine);
      this.outReviews = this.inReviews.filter((rev) =>
         rev.title.toLowerCase().indexOf(this.movieTitle.toLowerCase()) > -1
      );
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
