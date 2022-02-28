<template>
  <div>
    <h1>Search for the authors</h1>
    <div style="margin-bottom:30px">
      <input class="txtSearch" type="text" name="txtSearch" v-model="txtSearch" >
      <button @click="searchAuthor">Search</button>
    </div>

    <div class="section-author-list" v-if="step=='authorList'">
      <div class="author-list-holder">
        <div class="author-list-item" v-for="author in authors.docs">
            <p><strong>Name:</strong> {{author.name}}</p>
            <p><strong>Works:</strong> {{author.work_count}}</p>
            <button class="small-btn" @click="getAuthorWork(author)">Get Works</button>
        </div>
      </div>
    </div>

    <div class="section-work-list" v-if="step=='workList'">
      <h3>Work list of "{{selectedAuthor.name}}"</h3>
      <button class="small-btn" @click="backToAuthorList">Back To Authors</button>
      <div class="work-list-holder">
        <div class="work-list-item" v-for="work in works.entries">
            <p><strong>Title:</strong> {{work.title}}</p>
            <p><strong>Work ID:</strong> {{work.key}}</p>
            <button class="small-btn" @click="getWorkDetail(work)">Get Details</button>
        </div>
      </div>
    </div>

    <div class="section-work-info" v-if="step=='workInfo'">
      <div class="work-info-holder">
        <div class="cover-img" >
          <img :src="getCoverImg(selectedWork)" :alt="selectedWork.title">
        </div>
        <div class="work-details">
          <h2>Title: {{selectedWork.title}}</h2>
          <p><strong>Author:</strong> {{selectedAuthor.name}}</p>
          

          <p v-if="selectedWork.first_publish_date"><strong>First Publish Date:</strong> {{selectedWork.first_publish_date}}</p>
          <p v-else><strong>First Publish Date:</strong> not available</p>

          <div v-if="selectedWork.subjects">
            <p><strong>Subjects:</strong></p>
            <ul class="subject-list"> 
              <li v-for="subject in selectedWork.subjects">
                {{subject}}
              </li>
            </ul>
          </div>
          <p v-else><strong>Subjects:</strong> not available</p>
          
          <p v-if="selectedWork.description"><strong>Description:</strong>
          {{selectedWork.description.value}}</p>
          <p v-else><strong>Description:</strong> not available</p>

        </div>
      </div>
      <button @click="backToWorkList">Back To Works</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      txtSearch:'',
      step:'search',
      authors: {},
      selectedAuthor:{},
      works:{},
      selectedWork:{},
      cover:{},
    }
  },
  methods: {
    /*get author list on button click*/
    async searchAuthor() {
      this.step='authorList';
      if(this.txtSearch!=''){
        this.authors = await this.$http.$get(
          `https://openlibrary.org/search/authors.json?q=${this.txtSearch}`
        );
      }
    },

    backToAuthorList(){
      this.step='authorList';
    },

    /*get work list for specific author*/
    async getAuthorWork(authorItem) {
      this.step='workList';
      this.selectedAuthor=authorItem;
      
      this.works = await this.$http.$get(
        `https://openlibrary.org/authors/${authorItem.key}/works.json`
      );
    },

    backToWorkList(){
      this.step='workList';
    },

    getCoverImg(workItem){
        //find coverID
        let finalCovers = workItem.covers;
        if (!Array.isArray(workItem.covers)) {
          finalCovers = [workItem.covers];
        }
        let iterator = 0;
        let coverId= finalCovers[iterator];
        while (coverId === -1) {
          coverId = workItem.covers[iterator++];
        }

        return "https://covers.openlibrary.org/b/id/"+coverId+"-L.jpg";
    },

    /*get details for specific work*/
    getWorkDetail(workItem) {
      this.step='workInfo';
      this.selectedWork=workItem;

    }
  }
}
</script>
