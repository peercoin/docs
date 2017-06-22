<div class="MainComp">
  <Topbar ref:topbar on:mobilemenu="handleMobileMenu(event)" on:fontsize="handleFontSize(event)" />
  <Menu ref:menu on:mobilemenu="handleMobileMenu(event)" />
  <div class="warn">Disclaimer:<br>This documentation is a work in progress. It isn't ready and shouldn't be shared with outsiders until the removal of this message. If you want to help build it, please <a href="https://github.com/peercoin/docs#peercoin-official-documentation-repository">click here</a>.</div>
  <div class="doc-container font-{{fontSize}}" ref:docContainer>
    {{{ documentationHTML }}}
  </div>
</div>

<script>
  import Settings from '../herodotus-settings.js';
  import Menu from './menu.component';
  import Topbar from './topbar.component';
  import marked from 'marked';
  import ajax from '@fdaciuk/ajax';
  //import Prism from 'prismjs';

  export default {
    oncreate () {
      this.registerDocumentation();
    },

    data () {
      return {
        fontSize: 2,
        documentation: '',
        documentationHTML: ''
      }
    },

    components: {
      Menu,
      Topbar
    },

    methods: {
      handleFontSize (event) {
        let action = event.action;
        switch (action) {
          case 'INCREASE':
          this.increaseFont();
          break;
          case 'DECREASE':
          this.decreaseFont();
          break;
        }
      },
      handleMobileMenu (event) {
        let action = event.action;
        switch (action) {
          case 'TOGGLE':
          this.refs.topbar.set({isMenuOpen: this.refs.menu.toggle()});
          break;
          case 'CLOSE':
          this.refs.menu.close();
          break;
          case 'OPEN':
          this.refs.menu.open();
          this.refs.topbar.set({isMenuOpen: true});
          break;
        }
      },
      increaseFont () {
        let fontSize = this.get('fontSize');
        if (fontSize >= 4) {
          return;
        }
        this.set({fontSize: fontSize + 1});
      },
      decreaseFont () {
        let fontSize = this.get('fontSize');
        if (fontSize <= 1) {
          return;
        }
        this.set({fontSize: fontSize - 1});
      },
      registerDocumentation () {
        let DOC_URL;
        
        if(Settings.allow_remote_documentation) {
          DOC_URL = Settings.remote_documentation_url;
        } else {
          DOC_URL = 'documentation.md';
        }

        ajax().get(DOC_URL).then((res, xhr) => {
          // Print documentation HTML
          this.set({
            documentation: res,
            documentationHTML: marked(res)
          });

          // Send menu to menu component
          this.refs.menu.startMenu(this.generateMenu());

          // Highlight code
          //Prism.highlightAll();
        });
      },
      generateMenu () {
        let docElements = this.refs.docContainer;
        let headingItems = docElements.querySelectorAll('h1, h2');
        let menuItems = [];
        let menuItemsFlat = [];
        let currH1;

        headingItems.forEach((item) => {
          menuItemsFlat.push({
            type: item.nodeName.toLowerCase(),
            label: item.textContent,
            id: item.id
          });

          if (item.nodeName.toLowerCase() === 'h1') {
            menuItems.push({
              type: item.nodeName.toLowerCase(),
              label: item.textContent,
              id: item.id
            });
            currH1 = menuItems[menuItems.length - 1];
            currH1.children = [];
            return;
          } else if (item.nodeName.toLowerCase() === 'h2') {
            currH1.children.push({
              type: item.nodeName.toLowerCase(),
              label: item.textContent,
              id: item.id
            });
          }
        });

        return {menuItems: menuItems, menuItemsFlat: menuItemsFlat};
      }
    }
  }
</script>