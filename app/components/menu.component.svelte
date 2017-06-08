<div>
  <div class="MenuComp--overlay {{(isOpen) ? 'active' : ''}}" ref:overlay on:click="fire('mobilemenu', {action: 'CLOSE'})"></div>
  <div class="MenuComp {{(isOpen) ? 'open' : ''}}" ref:menu>
    <div class="logo" on:click="scrollTop()">
      <img src="img/logo.svg" alt="PeerAssets WhitePaper">
    </div>
    <ul class="menu">
      {{#each menuItems as item}}
        <li class="{{(item.active) ? 'active ' : ''}}{{item.type}}">
          <a on:click="scrollToItem(item, event)" href="#{{item.id}}">{{item.label}}</a>
            {{#if item.children.length > 0}}
              <ul>
                {{#each item.children as subitem}}
                  <li class="{{(subitem.active) ? 'active ' : ''}}{{subitem.type}}">
                    <a on:click="scrollToItem(subitem, event)" href="#{{subitem.id}}">{{subitem.label}}</a>
                  </li>
                {{/each}}
              </ul>
            {{/if}}
        </li>
      {{/each}}
    </ul>
  </div>
</div>

<script>
  export default {
    oncreate () {
      //this.on('', () => {

      //});
    },

    data () {
      return {
        menuItems: [],
        menuItemsFlat: [],
        isOpen: false,
        prevY: 0
      }
    },

    methods: {
      startMenu (menuOpts) {
        this.set(menuOpts);
        setTimeout(() => {
          this.handleActivatedMenuOnScroll();
          this.scrollToURLMenu();
        }, 10);
      },
      scrollTop() {
        window.scrollTo(0, 0);
      },
      scrollToURLMenu () {
        let hash = window.location.hash.substr(2);
        let filtered = this.get('menuItemsFlat').filter(item => item.id === hash);

        if (filtered) {
          let heading = document.getElementById(filtered[0].id);
          let top = window.scrollY + heading.getBoundingClientRect().top - 70;
          window.scrollTo(0, top);
        }
      },
      toggle () {
        this.set({isOpen: !this.refs.menu.isOpen});
        return this.refs.menu.isOpen;
      },
      close () {
        this.set({isOpen: false});
      },
      open () {
        this.set({isOpen: true});
      },
      handleSubSections () {
        //let currentActive = document.querySelector('.active ~');
      },
      activeClass (active) {
        if(active === true) {
          return 'active';
        } else {
          return '';
        }
      },
      removeActiveState () {
        let menuItems = this.get('menuItemsFlat').map(item => {
          item.active = false;
          return item;
        });
        this.set({menuItemsFlat: menuItems});
      },
      handleActivatedMenuOnScroll () {
        let menuItems = this.get('menuItemsFlat');

        window.onscroll = (e) => {
          let currY = window.scrollY;
          let stop = false;

          menuItems.forEach((item, i) => {
            let currTop = window.scrollY + document.getElementById(item.id).getBoundingClientRect().top - 120;
  
            if (stop) {
              return;
            }

            if (i <= 0) {
              i = 1;
            }

            if (currTop > window.scrollY) {
              this.removeActiveState();
              if ((window.innerHeight + window.scrollY) >= document.body.offsetHeight) {
                menuItems[menuItems.length-1].active = true;
              } else {
                menuItems[i-1].active = true;
              }
              stop = true;
            } else {
              item.active = false;
            }
          });

          this.set({
            menuItemsFlat: menuItems,
            prevY: currY
          });
        }
      },
      scrollToItem (item, e) {
        if(e) {
          e.preventDefault();
        }

        window.location.hash = '/' + item.id;
        let menuItems = this.get('menuItemsFlat');
        let top = window.scrollY + document.getElementById(item.id).getBoundingClientRect().top - 70;
        window.scrollTo(0, top);

        // If reached bottom
        this.removeActiveState();
          menuItems.map(loopItem => {
            if(loopItem == item) {
              loopItem.active = true;
            }
            return loopItem;
          });   

        this.fire('mobilemenu', {action: 'CLOSE'});
        this.set({menuItemsFlat: menuItems});
      }
    }
  }
</script>