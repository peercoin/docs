<div class="SearchListComp">
  <svg class="svg-icon" xmlns="http://www.w3.org/2000/svg" role="img" viewBox="0 0 15 15">
    <use xlink:href="img/icon-search.svg#icon" preserveAspectRatio="xMidYMid" />
  </svg>

  <div class="search-popup">
    <input type="text" class="filter-input" on:input="handleSearch(event)">
    {{#if filteredList.length > 1 }}
    <ul class="filtered-list">
      {{#each filteredList as item}}
      <li class="item">
        <div class="section-title">{{item.item.title}}</div>
        <div class="section-text">{{item.item.content.substr(0, 100)}}...</div>
      </li>
      {{/each}}
    </ul>
    {{/if}}

    {{#if filteredList.length < 1 }}
      <h2 class="empty-message">No matches found.</h2>
    {{/if}}
  </div>
</div>

<script>
  import Fuse from 'fuse.js';

  export default {
    oncreate() {
      this.observe('searchList', (list) => {
        this.fuse = this.setFuse(list);
      });
    },
    data() {
      return {
        searchList: [],
        filteredList: [],
        fuse: null
      }
    },
    methods: {
      setFuse(searchList) {
        if(searchList.length < 1) {
          return;
        }
        this.set({
          fuse: new Fuse(searchList, {
            shouldSort: true,
            findAllMatches: true,
            includeMatches: true,
            threshold: 0.3,
            location: 0,
            distance: 1000,
            maxPatternLength: 32,
            minMatchCharLength: 3,
            keys: [
              "content"
            ]
          })
        });
      },
      handleSearch(e) {
        const text = e.target.value;
        if(text.length > 3) {
          this.set({
            filteredList: this.get('fuse').search(e.target.value)
          });
        } else {
          this.set({
            filteredList: []
          });
        }
        console.log(this.get('filteredList'));
      }
    }
  }
</script>