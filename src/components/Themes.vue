<template>
     <div class="themes-page">
       <h1>All Themes</h1>
        <!--Sidebar -->
        <section class="sidebar">
            <input type="text" v-model="searchQuery" placeholder="Search" /> 
              <select v-model="selectedCategory" >
                <option  value="All" >All</option>
                <option  value="free" >Free </option>
                <option  value="freemium" >Freemium</option>
                <option value="premium" >Premium</option>
              </select>
        </section>
        <!--Main Content -->
        <section class="entry-content">
          <template v-if="searchQuery">
            <ul class="themes-data">
              <!--Show Search query results -->
                <li v-for="themeData in searchResults" :key="themeData.id">
                    <div class="theme-info">
                        <h2 class="theme-title">{{themeData.title}}</h2>
                        <div class="theme-metadata">
                            <p>status: {{themeData.status}}</p>
                            <p>category: {{themeData.category}}</p>
                        </div>
                    </div>
                </li>
            </ul>
          </template>
            <template v-else-if="selectedCategory!=='All'"> 
            <ul class="themes-data">
              <!--Show DropDown filter results -->
                <li v-for="themeData in filteredThemes" :key="themeData.id">
                    <div class="theme-info">
                        <h2 class="theme-title">{{themeData.title}}</h2>
                        <div class="theme-metadata">
                          <p>status: {{themeData.status}}</p>
                          <p>category: {{themeData.category}}</p>
                        </div>
                    </div> 
                </li>
            </ul>
            </template>
            <template v-else> 
              <ul class="themes-data">
              <!--Show default results -->
                <li v-for="themeData in paginatedThemesList" :key="themeData.id">
                    <div class="theme-info">
                        <h2 class="theme-title">{{themeData.title}}</h2>
                        <div class="theme-metadata">
                            <p>status: {{themeData.status}}</p>
                            <p>category: {{themeData.category}}</p>
                        </div>
                    </div>
                </li>
            </ul>
             <!--     Loop through the pages array to display each page number       -->
              <section class="pagination">
                <button type="button" class="btn btn-sm btn-outline-secondary" v-if="page != 1" @click="page--"> Previous </button>
                <button type="button" class="btn btn-sm btn-outline-secondary" v-for="pageNumber in pages.slice(page-1, page+5)" @click="page = pageNumber" :key="pageNumber"> {{pageNumber}} </button>
                <button type="button" @click="page++" v-if="page < pages.length" class="btn btn-sm btn-outline-secondary"> Next </button>
              </section>
            </template>
        </section>
         <!-- End of Main Content -->
    </div>
</template>

<script>
export default {
  name: 'Themes',
    data() {
    return {
      page: 1,
      perPage: 6,
      pages: [],
      searchQuery:'',
      selectedCategory: "All", 
      themesList: []
    };
    },
    
    created() {
      fetch("themes.json")
        .then(response => response.json())
        .then(data => (this.themesList = data));
        },

    watch: {
      themesList () {
        this.setPages();
      }
    },
    
    computed: {

    searchResults (){
      if(this.searchQuery){
        //Search themes by title. Case insensitive.
      return this.themesList.filter((theme)=>{
        return theme.title.toLowerCase().startsWith(this.searchQuery.toLowerCase());
      })
      }else{
        return this.themesList;
      }
    },

    filteredThemes() {
      var category = this.selectedCategory;
      //Filter themes by Category
      console.log(category);
			if(category === "All") {
        
                //save performance, just return the default array:
				return this.themesList;
			} else {
				return this.themesList.filter(function(themes) {
					//return the array after passimng it through the filter function:
					return  (category === 'All' || themes.category === category);	 

				});
			}
    },

    paginatedThemesList () {
      return this.paginate(this.themesList);
    }
    
  },
  methods: {
    setPages () {
      let numberOfPages = Math.ceil(this.themesList.length / this.perPage);
      for (let index = 1; index <= numberOfPages; index++) {
        this.pages.push(index);
      }
    },
    paginate (themesList) {
      let page = this.page;
      let perPage = this.perPage;
      let from = (page * perPage) - perPage;
      let to = (page * perPage);
      return  themesList.slice(from, to);
    },
  }   
}
</script>

<style>
.themes-page{
    display: block;
    margin: 0 auto;
    width: 65%;
}
.themes-data {
  list-style: none;
  display: flex;
  flex-wrap:wrap;
  width:100%;
}
.themes-data li{
    width: 33%;
    margin: 15px 0px;
    display: block;
    margin: 0 auto;
}

.sidebar > * {
    margin: 15px;
}
</style>