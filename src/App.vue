<template>
  <v-app>
    <v-navigation-drawer
      fixed
      :mini-variant="miniVariant"
      :clipped="clipped"
      v-model="drawer"
      app
    >
      <v-list>
        <v-list-tile
          value="true"
          v-for="(item, i) in items"
          :key="i"
        >
          <v-list-tile-action>
            <v-icon v-html="item.icon"></v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title v-text="item.title"></v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    <v-toolbar fixed app :clipped-left="clipped">
      <v-toolbar-side-icon @click.stop="drawer = !drawer"></v-toolbar-side-icon>
      <v-btn icon @click.stop="miniVariant = !miniVariant">
        <v-icon v-html="miniVariant ? 'chevron_right' : 'chevron_left'"></v-icon>
      </v-btn>
      <v-btn icon @click.stop="clipped = !clipped">
        <v-icon>web</v-icon>
      </v-btn>
      <v-btn icon @click.stop="fixed = !fixed">
        <v-icon>remove</v-icon>
      </v-btn>
      <v-toolbar-title v-text="title"></v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn icon @click.stop="rightDrawer = !rightDrawer">
        <v-icon>menu</v-icon>
      </v-btn>
    </v-toolbar>
    <v-content>
      <v-container fluid>
          <v-layout column align-center>
            <template>
              <div>
                <form>
                  <div>Blog Post:</div>
                  <br>
                  <v-text-field
                  label="Title"
                  v-model="blogtitle"
                  placeholder="Add a Blog Title"

                  ></v-text-field>
                  <br>
                  <v-text-field
                  label="Post"
                  v-model="blogpost"
                  placeholder="Add the Post"

                  ></v-text-field>
                  <br>
                  <v-text-field
                  label="Posted"
                  v-model="blogposted"
                  placeholder="Today"
                  disabled
                  ></v-text-field>
                  <br>
                  <v-btn @click="submit">submit</v-btn>
                  <v-btn @click="clear">clear</v-btn>
                  <br>
                </form>

              </div>
            </template>
          </v-layout>
            <br>
          <v-layout column align-center>
            <template>
              <div>
                  <br>
                  <div>Blog Post List:</div>
                  <br>
                    <ul>
                      <li v-for="(item, index) in itemls" >

                        Title: {{  item.title }} <br>
                        Post: {{  item.post }} <br>
                        Posted: {{  item.posted }} <br>
                         <v-btn @click="removeit(index)"> Delete </v-btn>
                         <v-btn @click="editit(index)"> Edit </v-btn><br>
                      </li>
                    </ul>

                  <br>
                </div>
              </template>
          </v-layout>

      </v-container>
    </v-content>

    <v-footer :fixed="fixed" app>
      <span>&copy; 2017</span>
    </v-footer>
  </v-app>
</template>

<script>
  export default {
    data () {
      return {
        clipped: false,
        miniVariant: false,
        drawer: true,
        fixed: false,
        items: [ ],
        title: 'Blog - Lee',
        //blogpost: '',
        itemls: [{ title: 'Or Not', post: ' This maybe okay ', posted: 'Today'}],
        blogtitle: '',
        blogpost: '',
        blogposted: '',
        blogedit: 0,
        blogredux: '',

        blogtitle: ''

      }
    }
  ,
  methods: {
    submit : function() {
        //alert("hello");
        //console.log(this.blogedit + ' - before');
     if(this.blogedit > 0){
       this.blogredux = "{ title:" + this.blogtitle + ', post: ' + this.blogpost + ', posted: ' + 'Today'+ "}";
       //console.log(this.blogredux);
       //console.log(this.blogedit);
       //this.itemls.splice(this.blogedit, 1,this.blogredux)
       this.itemls[this.blogedit].title = this.blogtitle;
       this.itemls[this.blogedit].post = this.blogpost;
       this.itemls[this.blogedit].posted = 'Today';

       //this.itemls.$set(this.blogedit, this.blogredux)
    }else {
      this.itemls.push({
        title: this.blogtitle,
        post: this.blogpost,
        posted: 'Today'
      })
      //this.blogtitle = '';
      //this.blogpost = '';

    }
    this.blogtitle = '';
    this.blogpost = '';
    },
    clear : function() {
        //this.form.reset()
        this.blogtitle = '';
        this.blogpost = '';

    },
    removeit : function(index) {
      
      this.itemls.splice(index, 1);
    }
    ,
    editit : function(index) {
      //alert(index);
      this.blogtitle = this.itemls[index].title;
      this.blogpost = this.itemls[index].post;

      this.blogedit = index;

    }
  }

  }
</script>
